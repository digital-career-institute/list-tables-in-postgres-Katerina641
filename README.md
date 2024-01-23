# Exercise # 1 - List Tables in a PostgreqSQL Database

> **Create a Java Application, "TableLister" that connects to the PostgreqSQL database on localhost and list out names of all Tables**

***Hint:*** 
- Download JDBC Driver library for PostgreqSQL
-- Search on internet for the above.
- Add this to the classpath
- Create an instance of *Connection* using *DriverManager* API
-- Specify the URL with specified database, username and password appropriately
- Get hold of *DatabaseMetaData* from the *Connection* object
- Use *getTables* method on above to find the list of tables 
-- Note: Filter out everything which is not a table, technically
- Display the gathered values as the list of Tables
package DatabaseLister;

import java.beans.Statement;
import java.sql.Connection;
import java.sql.DatabaseMetaData;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;

public class main {

	public static void main(String[] args) throws ClassNotFoundException, SQLException {

		Connection connection = null;
		Class.forName("org.postgresql.Driver");
		connection = DriverManager.getConnection("jdbc:postgresql://localhost:5432/test", "postgres", "123456pas");
		java.sql.Statement st = connection.createStatement();

		// ResultSet rs = st.executeQuery("SELECT * FROM pg_catalog.pg_tables");

		Connection jdbcConnection = DriverManager.getConnection("jdbc:postgresql://localhost:5432/test", "postgres",
				"123456pas");
		DatabaseMetaData m = jdbcConnection.getMetaData();
		String[] types = { "TABLE" };
		ResultSet rs = m.getTables(null, null, "%", types);
		while (rs.next()) {
			System.out.println(rs.getString("TABLE_NAME"));
		}
		rs.close();
		rs.close();

		if (connection != null) {
			System.out.println("ok");
		} else {
			System.out.println("no");
		}

		try {

		} catch (Exception e) {
			System.out.println(e);

		}

	}

}

