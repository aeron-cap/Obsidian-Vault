- Java Database Connectivity which is an API for connecting and executing queries on a database.
- Can work on any database as long as proper drivers are provided.
- Several types of JDBC Drivers.
	1. Type 1 : contains mapping to another data access API (JDBC-ODBC driver).
	2. Type 2 : implementation that uses client-side libraries of the target database; native-API driver.
	3. Type 3 : uses middleware to convert JDBC calls into database-specific calls; also known as a network protocol driver.
	4. Type 4 : connect directly to a database by converting JDBC calls in to database-specific calls; database protocol drivers or thin drivers.
- To connect to a database, we simply have to initialize the driver and open a database connection. 
	1. Register the Driver
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.32</version>
</dependency>
<!-- next we register the driver using the Class.forName() method which dynamically loads the driver class -->
Class.forName("com.mysql.cj.jdbc.Driver");
<!-- In older versions of JDBC, before obtaining a connection, 
we first had to initialize the JDBC driver by calling the Class.forName method. 
As of JDBC 4.0, all drivers that are found in the classpath are automatically loaded. 
Therefore, we won’t need this Class.forName part in modern environments.
```
.
	2. Creating the Connection
	3. Executing SQL statements
		- The send SQL instructions to the database, we can use instances of type *Statement*, *PreparedStatement*, or *CallableStatement*, which we can obtain using the Connection object.
	4. Statements
		- Statement interface contains the essential functions for executing SQL commands.
		- executeQuery() for SELECT instructions
		- executeUpdate() for updating data or the database
		- execute() can be used for both cases when the result is unknown.
```java
try (Statement stmt = con.createStatement()) {
    // use stmt here
    String tableSql = "CREATE TABLE IF NOT EXISTS employees"
    + "(emp_id int PRIMARY KEY AUTO_INCREMENT, name varchar(30), " + "position varchar(30), salary double)";
    stmt.execute(tableSql);
    String insertSql = "INSERT INTO employees(name, position, salary)"
  + " VALUES('john', 'developer', 2000)";
stmt.executeUpdate(insertSql);
	//executeUpdate returns the number of affected rows.
	
	String selectSql = "SELECT * FROM employees"; 
	try (ResultSet resultSet = stmt.executeQuery(selectSql)) {
	    // use resultSet here
	}
	//we can use executeQuery to will return an object of type ResultSet.
	
	String updatePositionSql = "UPDATE employees SET position=? WHERE emp_id=?";
	try (PreparedStatement pstmt = con.prepareStatement(updatePositionSql)) {
	    // use pstmt here
		pstmt.setString(1, "lead developer");
		pstmt.setInt(2, 1);
		int rowsAffected = pstmt.executeUpdate();
	}
	//To add parameters to the _PreparedStatement_, we can use simple setters – _setX()_ – where _X_ is the type of the parameter, and the method arguments are the order and value of the parameter:
	
	String longRunningQuery = "SELECT SLEEP(15)"; // Simulating a long-running query
	assertThrows(SQLException.class, () -> {
		try (PreparedStatement pstmt = con.prepareStatement(longRunningQuery)) {
			pstmt.setQueryTimeout(5);
			pstmt.executeQuery();
		}
	});
	//**We can also set a timeout for the _PreparedStatement_ to limit how long the query can run before it is automatically cancelled**. This is useful in scenarios where we want to avoid long-running queries that may block the system.
	
	String preparedSql = "{call insertEmployee(?,?,?,?)}";
	try (CallableStatement cstmt = con.prepareCall(preparedSql)) {
	    // use cstmt here
	    cstmt.setString(2, "ana");
		cstmt.setString(3, "tester");
		cstmt.setDouble(4, 2000);
		cstmt.registerOutParameter(1, Types.INTEGER);
		cstmt.execute();
		int new_id = cstmt.getInt(1);
	}
	//for this aboce code to work, we need to create the stored procedure in our mysql databse
	delimiter //
	CREATE PROCEDURE insertEmployee(OUT emp_id int, 
	  IN emp_name varchar(30), IN position varchar(30), IN salary double) 
	BEGIN
	INSERT INTO employees(name, position,salary) VALUES (emp_name,position,salary);
	SET emp_id = LAST_INSERT_ID();
	END //
	delimiter ;
	
	GRANT ALL ON mysql.proc TO 'user1';
	//To be able to run a stored procedure from Java, the connection user needs to have access to the stored procedure’s metadata. This can be achieved by granting rights to the user on all stored procedures in all databases:
}
```
.
	5. Parsing query results
		- After executing a query, the result is represented by a _ResultSet_ object, which has a structure similar to a table, with lines and columns.
		- ResultSet interface
			- Create Employee class along with standard constructor, getter and setter
			- traverse the ResultSet and create an Employee object for each record
			- Retrieving the value for each table cell can be done using methods of type _getX(_) where X represents the type of the cell data.
			- The _getX()_ methods can be used with an _int_ parameter representing the order of the cell, or a _String_ parameter representing the name of the column. The latter option is preferable in case we change the order of the columns in the query.
		- Update ResultSet
			- ResultSet object can only bre traversed forward and cannot be modified.
			- To navigate this type of _ResultSet_, we can use one of the methods:
				- first(), last(), beforeFirst(), beforeLast() – to move to the first or last line of a _ResultSet_ or to the line before these
				- next(), previous() – to navigate forward and backward in the _ResultSet_
				- getRow() – to obtain the current row number
				- moveToInsertRow(), moveToCurrentRow() – to move to a new empty row to insert and back to the current one if on a new row
				- absolute(int row) – to move to the specified row
				- relative(int nrRows) – to move the cursor the given number of rows
			- To persist the _ResultSet_ changes to the database, we must further use one of the methods:
				- updateRow() – to persist the changes to the current row to the database
				- insertRow(), deleteRow() – to add a new row or delete the current one from the database
				- refreshRow() – to refresh the ResultSet with any changes in the database
				- cancelRowUpdates() – to cancel changes made to the current row
	6. Parsing Metadata
		- The JDBC API allows looking up information about the database, called metadata.
```java
DatabaseMetaData dbmd = con.getMetaData();
ResultSet tablesResultSet = dbmd.getTables(null, null, "%", null);
while (tablesResultSet.next()) {
    LOG.info(tablesResultSet.getString("TABLE_NAME"));
}
```
.
		- This interface can be used to find information about a certain _ResultSet_, such as the number and name of its columns:
```java
ResultSetMetaData rsmd = rs.getMetaData();
int nrColumns = rsmd.getColumnCount();

IntStream.range(1, nrColumns).forEach(i -> {
    try {
        LOG.info(rsmd.getColumnName(i));
    } catch (SQLException e) {
        e.printStackTrace();
    }
});
```
.
	7. Handling Transactions
		- By default, each SQL statement is committed right after it is completed. It is also possible to control transactions programmatically.
		- set autoCommit() property to false
```java
	String updatePositionSql = "UPDATE employees SET position=? WHERE emp_id=?";
PreparedStatement pstmt = con.prepareStatement(updatePositionSql);
pstmt.setString(1, "lead developer");
pstmt.setInt(2, 1);

String updateSalarySql = "UPDATE employees SET salary=? WHERE emp_id=?";
PreparedStatement pstmt2 = con.prepareStatement(updateSalarySql);
pstmt.setDouble(1, 3000);
pstmt.setInt(2, 1);

boolean autoCommit = con.getAutoCommit();
try {
    con.setAutoCommit(false);
    pstmt.executeUpdate();
    pstmt2.executeUpdate();
    con.commit();
} catch (SQLException exc) {
    con.rollback();
} finally {
    con.setAutoCommit(autoCommit);
}
```
.
	8. Closing the Resources
		- When we no longer use it, we need to close the connection to release the database resources.
		- `con.close();`
		- However, if we’re using the resource in a _try-with-resources_ block, we don’t need to call the _close()_ method explicitly, as the _try-with-resources_ block does that for us automatically.
		- **The same is true for the _Statements, PreparedStatements, CallableStatements, and ResultSets.**
