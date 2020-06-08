package accesoBD;

import com.mysql.jdbc.Connection;
import java.sql.*;

/**
 *
 * @author Sergio
 */
public class Conexion {

    java.sql.Connection conectar = null;

    public Conexion(){
        try {
             Class.forName("com.mysql.jdbc.Driver");
             conectar = DriverManager.getConnection("jdbc:mysql://localhost/blog","root","");
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }   
    }
    
    public java.sql.Connection getConection(){
    
     return conectar;}
           
    public void desconectar(){
    conectar=null;
    
    }
    
    
    
}
