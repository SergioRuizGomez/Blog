/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package DAO;

import accesoBD.Conexion;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.ArrayList;
import javax.swing.JOptionPane;
import Modelo.usuario;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;

/**
 *
 * @author Sergio
 */
 class DAOusuario implements Operaciones {
        usuario usuario = new usuario();

    @Override
    public boolean agregar(Object obj) {
  usuario = (usuario) obj;

        Conexion conn = new Conexion();
        Connection database = conn.getConection();
       
        String sql = "INSERT INTO usuario (nombreCompleto,correo,contraseña,telefono,avatar) VALUES (?,?,?,?,?)";
      
        PreparedStatement pst = null;
        try {

            pst = database.prepareStatement(sql);
            pst.setString(1, usuario.getNombre());
            pst.setString(2, usuario.getContrasena());
            pst.setString(3, usuario.getCorreo());
            pst.setString(4, usuario.getTelefono());
            pst.setString(5, usuario.getAvatar());

            int filas = pst.executeUpdate();

            if (filas > 0) {
                database.close();
                return true;

            } else {

                database.close();
                return false;

            }
        } catch (SQLException  e) {
            JOptionPane.showMessageDialog(null, "Error, Verifique la información" + e.getMessage());
            return false;
        }
    }

    @Override
    public boolean modificar(Object obj) { //sergio
          usuario = (usuario) obj;

        Conexion conn = new Conexion();
        Connection database = conn.getConection();
      
        String sql = "UPDATE usuario SET nombreCompleto = ?, correo = ?, contraseña = ?, telefono = ?, avatar = ?  WHERE id = ?";
        
        PreparedStatement pst = null;
        try {

            pst = database.prepareStatement(sql);
            pst.setString(1, usuario.getNombre());
            pst.setString(2, usuario.getCorreo());
            pst.setString(3, usuario.getContrasena());
            pst.setString(4, usuario.getTelefono());
            pst.setString(5, usuario.getAvatar());
            pst.setInt(6, usuario.getId());

            int filas = pst.executeUpdate();

            if (filas > 0) {
                database.close();
                return true;

            } else {

                database.close();
                return false;

            }
        } catch (SQLException  e) {
            JOptionPane.showMessageDialog(null, "Error, Verifique la información" + e.getMessage());
            return false;

        }   
        
    }

    @Override
    public boolean eliminar(Object obj) {
   usuario = (usuario) obj;

        Conexion conn = new Conexion();
        Connection database = conn.getConection();
        

        String sql = "DELETE FROM usuarios WHERE id = ?";
   
        PreparedStatement pst = null;
        try {

            pst = database.prepareStatement(sql);
            pst.setInt(1, usuario.getId());
      
            int filas = pst.executeUpdate();

            if (filas > 0) {
                database.close();
                return true;

            } else {

                database.close();
                return false;

            }
        } catch (SQLException  e) {
            JOptionPane.showMessageDialog(null, "Error, Verifique la información" + e.getMessage());
            return false;

        }

        
        
            }

    @Override
    public ArrayList<Object[]> consultar() {
   
        String sql = "SELECT * FROM usuario";
         Conexion conn = new Conexion();
        Connection database = conn.getConection();
        PreparedStatement pst = null;
        ResultSet rs;
        ResultSetMetaData meta;
        ArrayList<Object[]> datos = new ArrayList<>();

        try {
              pst = database.prepareStatement(sql);
            rs = pst.executeQuery();
            meta = rs.getMetaData();
            while (rs.next()) {
                Object[] fila = new Object[meta.getColumnCount()];
                for (int i = 0; i < fila.length; i++) {

                    fila[i] = rs.getObject(i + 1);
                }
                datos.add(fila);
            }
        } catch (SQLException e) {
            JOptionPane.showMessageDialog(null, "ocurrio un error" + e.getMessage());
        }
        return datos;

}
}