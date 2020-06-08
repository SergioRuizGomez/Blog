/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package DAO;

import Modelo.usuario;
import java.util.ArrayList;
import accesoBD.Conexion;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import javax.swing.JOptionPane;
import Modelo.comentario;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;

/**
 *
 * @author Sergio
 */
class DAOcomentario implements Operaciones {

    comentario comentario = new comentario();
    Conexion conn = new Conexion();
    Connection database = conn.getConection();

    @Override
    public boolean agregar(Object obj) {
        comentario = (comentario) obj;

        Conexion conn = new Conexion();
        Connection database = conn.getConection();

        String sql = "INSERT INTO comentario (fechaHora,contenido,idUsuario) VALUES (?,?,?)";

        PreparedStatement pst = null;
        try {

            pst = database.prepareStatement(sql);
            pst.setString(1, comentario.getFechaHora());
            pst.setString(2, comentario.getContenido());
            pst.setInt(3, comentario.getIdUsuario());

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

        comentario = (comentario) obj;

        Conexion conn = new Conexion();
        Connection database = conn.getConection();

        String sql = "UPDATE comentario SET fechaHora = ?, contenido = ?, idUsuario = ? WHERE id = ?";

        PreparedStatement pst = null;
        try {

            pst = database.prepareStatement(sql);
            pst.setString(1, comentario.getFechaHora());
            pst.setString(2, comentario.getContenido());
            pst.setInt(3, comentario.getIdUsuario());
            pst.setInt(4, comentario.getId());

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
        comentario = (comentario) obj;

        Conexion conn = new Conexion();
        Connection database = conn.getConection();

        String sql = "DELETE FROM comentario WHERE id = ?";

        PreparedStatement pst = null;
        try {

            pst = database.prepareStatement(sql);
            pst.setInt(1, comentario.getId());

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

        String sql = "SELECT * FROM comentarios";
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
