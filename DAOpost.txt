/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package DAO;

import Modelo.comentario;
import accesoBD.Conexion;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.SQLException;
import java.util.ArrayList;
import javax.swing.JOptionPane;
import Modelo.post;

/**
 *
 * @author Sergio
 */
class DAOpost implements Operaciones {

    post post = new post();

    Conexion conn = new Conexion();
    Connection database = conn.getConection();

    public boolean agregar(Object obj) {
        post = (post) obj;

        Conexion conn = new Conexion();
        Connection database = conn.getConection();

        String sql = "INSERT INTO post (fechaHoraCreacion,contenido,fechaHoraEdicion,idUsuario) VALUES (?,?,?,?)";

        PreparedStatement pst = null;
        try {

            pst = database.prepareStatement(sql);
            pst.setString(1, post.getFechaCreacion());
            pst.setString(2, post.getContenido());
            pst.setString(3, post.getFechaEdicion());
            pst.setInt(4, post.getIdUsuario());

            int filas = pst.executeUpdate();

            if (filas > 0) {
                database.close();
                return true;

            } else {

                database.close();
                return false;

            }
        } catch (SQLException e) {
            JOptionPane.showMessageDialog(null, "Error, Verifique la información" + e.getMessage());
            return false;
        }
    }

    @Override
    public boolean modificar(Object obj) { //sergio

        post = (post) obj;

        Conexion conn = new Conexion();
        Connection database = conn.getConection();

        String sql = "UPDATE post SET fechaHoraCreacion = ?, contenido = ?, fechaHoraEdicion = ?, idUsuario = ? WHERE id = ?";

        PreparedStatement pst = null;
        try {

            pst = database.prepareStatement(sql);
            pst.setString(1, post.getFechaCreacion());
            pst.setString(2, post.getContenido());
            pst.setString(3, post.getFechaEdicion());
            pst.setInt(4, post.getIdUsuario());
            pst.setInt(5, post.getId());

            int filas = pst.executeUpdate();

            if (filas > 0) {
                database.close();
                return true;

            } else {

                database.close();
                return false;

            }
        } catch (SQLException e) {
            JOptionPane.showMessageDialog(null, "Error, Verifique la información" + e.getMessage());
            return false;

        }

    }

    @Override
    public boolean eliminar(Object obj) {
        post = (post) obj;

        Conexion conn = new Conexion();
        Connection database = conn.getConection();

        String sql = "DELETE FROM post WHERE id = ?";

        PreparedStatement pst = null;
        try {

            pst = database.prepareStatement(sql);
            pst.setInt(1, post.getId());

            int filas = pst.executeUpdate();

            if (filas > 0) {
                database.close();
                return true;

            } else {

                database.close();
                return false;

            }
        } catch (SQLException e) {
            JOptionPane.showMessageDialog(null, "Error, Verifique la información" + e.getMessage());
            return false;

        }

    }

    @Override
    public ArrayList<Object[]> consultar() {

        String sql = "SELECT * FROM post";
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
