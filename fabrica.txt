/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package DAO;

/**
 *
 * @author Sergio
 */
public class fabrica {

    private static DAOusuario usuarios;
    private static DAOpost post;
    private static DAOcomentario comentario;

    public static DAOusuario getDAOusuariostatic() {
        if (fabrica.usuarios == null) {
            fabrica.usuarios = new DAOusuario();

        }
        return fabrica.usuarios;
    }

    public static DAOpost getDAOpost() {
        if (fabrica.post == null) {
            fabrica.usuarios = new DAOusuario();

        }
        return fabrica.post;

    }

    public static DAOcomentario getDaOcomentario (){
    if (fabrica.comentario == null){
    fabrica.comentario =  new DAOcomentario();
    
    
    }
    return fabrica.comentario;
    
    
    }
    
    
}
