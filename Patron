package Model;

import com.mongodb.client.MongoCollection;

import java.util.ArrayList;
import java.util.List;
import java.util.Locale;

public class Patron {

    private static String patronOriginal;
    private static String direccionOriginal;

    private static List<String> valores = new ArrayList<>();

    public static void main(String[] args) {

        direccionOriginal = "AL FONDO A LA DERCHA 23, 5º A";
        patronOriginal = crearPatron(direccionOriginal);

        recortarPatron();
        ordenarValores();

        System.out.println("Patron Inici: " + patronOriginal);
        System.out.println("\nValores: \n");

        for (String valor : valores)
            System.out.println("Valor: " + valor);
    }


    public static String crearPatron(String direccion) {

        String patron = "^";
        char caracter = '.';
        char ultimoCaracter = '.';
        String actual = "";

        for (int i = 0; i < direccion.length(); i++) {
            caracter = direccion.charAt(i);

            if (Character.isDigit(caracter)) caracter = '0';
            else if (caracter == 'º') caracter = '/';
            else if (Character.isAlphabetic(caracter)) caracter = 'a';

            switch (caracter){

                case '0':
                    if (ultimoCaracter == '0'){
                        //System.out.println("Metemos: [0-9]+ " + i);
                        actual = "[0-9]+";
                    }  else if (ultimoCaracter == 'a') {
                        patron += actual;
                        actual = "[A-Za-z]";
                    } else {
                        //System.out.println("Metemos: [0-9] " + i);
                        actual = "[0-9]";
                    }
                    break;
                case 'a':
                    if (ultimoCaracter == 'a') {
                        actual = "[A-Za-z]+";
                    } else if (ultimoCaracter == '0') {
                        patron += actual;
                        actual = "[A-Za-z]";
                    } else {
                        actual = "[A-Za-z]";
                    }
                    break;
                case ',':
                    patron += actual;
                    patron += "[,]";
                    actual = "";
                    break;
                case ' ':
                    patron += actual;
                    patron += "[ ]";
                    actual = "";
                    break;
                default:
                    patron += actual;
                    patron += ".*";
                    actual = "";
                    break;
            }

            if (i == (direccion.length() - 1))
                patron += actual;

            ultimoCaracter = caracter;
        }

        patron += "$";

        return patron;
    }
    public static String crearPatronCorto(String direccion) {

        String patron = "^";
        char caracter = '.';
        char ultimoCaracter = '.';
        String actual = "";

        for (int i = 0; i < direccion.length(); i++) {
            caracter = direccion.charAt(i);

            if (Character.isDigit(caracter)) caracter = '0';
            else if (caracter == ' ') caracter = 'a';
            else if (Character.isAlphabetic(caracter)) caracter = 'a';

            switch (caracter){

                case '0':
                    if (ultimoCaracter == '0'){
                        //System.out.println("Metemos: [0-9]+ " + i + ", para: " + caracter);
                        actual = "[0-9]+";
                    }  else if (ultimoCaracter == 'a') {
                        patron += actual;
                        actual = "[0-9]";
                    } else {
                        //System.out.println("Metemos: [0-9] " + i + ", para: " + caracter);
                        actual = "[0-9]";
                    }
                    break;
                case 'a':
                    if (ultimoCaracter == 'a') {
                        actual = "[A-Za-z ]+";
                    } else if (ultimoCaracter == '0') {
                        patron += actual;
                        actual = "[A-Za-z ]";
                    } else {
                        actual = "[A-Za-z ]";
                    }
                    //System.out.println("Metemos: [A-Za-z] " + i + ", para: " + caracter);
                    break;
                case ',':
                    patron += actual;
                    patron += "[,]";
                    actual = "";
                    //System.out.println("Metemos: [,] " + i + ", para: " + caracter);
                    break;
//                case ' ':
//                    patron += actual;
//                    patron += "[ ]";
//                    actual = "";
//                    System.out.println("Metemos: [ ] " + i + ", para: " + caracter);
//                    break;
                default:
                    patron += actual;
                    patron += "[.*]";
                    actual = "";
                    //System.out.println("Metemos: [^@] " + i + ", para: " + caracter);
                    break;
            }

            if (i == (direccion.length() - 1))
                patron += actual;

            ultimoCaracter = caracter;
        }

        patron += "$";

        return patron;
    }


    public static void recortarPatron() {

        String patron = patronOriginal.substring(1, patronOriginal.length() - 1);
        String direccion = direccionOriginal;

        while (patron.length() > 0) {

            String valor = "";

            System.out.println("patron: " + patron);
            System.out.println("direccion: " + direccion);

            if (nextIsLetras(patron)) {
                patron = patron.substring(9);
                switch (checkNext(patron)) {
                    case "[,]":
                        valor = direccion.substring(0, direccion.indexOf(","));
                        valores.add(valor);
                        direccion = direccion.substring(direccion.indexOf(","));
                        break;
                    case "[ ]":
                        valor = direccion.substring(0, direccion.indexOf(" "));
                        valores.add(valor);
                        direccion = direccion.substring(direccion.indexOf(" "));
                        break;
                    case ".*":
                        valor = direccion.substring(0, checkSimbolIndex(direccion));
                        valores.add(valor);
                        direccion = direccion.substring(checkSimbolIndex(direccion));
                        break;
                    default:
                        valores.add(direccion);
                        break;
                }
            }
            else if (nextIsLetra(patron)) {
                patron = patron.substring(8);
                switch (checkNext(patron)) {
                    case "[,]":
                        valor = direccion.substring(0, direccion.indexOf(","));
                        valores.add(valor);
                        direccion = direccion.substring(direccion.indexOf(","));
                        break;
                    case "[ ]":
                        valor = direccion.substring(0, direccion.indexOf(" "));
                        valores.add(valor);
                        direccion = direccion.substring(direccion.indexOf(" "));
                        break;
                    case ".*":
                        valor = direccion.substring(0, checkSimbolIndex(direccion) + 1);
                        valores.add(valor);
                        direccion = direccion.substring(checkSimbolIndex(direccion));
                        break;
                    default:
                        valores.add(direccion);
                        break;
                }
            }
            else if (nextIsNumeros(patron)) {
                patron = patron.substring(6);
                switch (checkNext(patron)) {
                    case "[,]":
                        valor = direccion.substring(0, direccion.indexOf(","));
                        valores.add(valor);
                        direccion = direccion.substring(direccion.indexOf(","));
                        break;
                    case "[ ]":
                        valor = direccion.substring(0, direccion.indexOf(" "));
                        valores.add(valor);
                        direccion = direccion.substring(direccion.indexOf(" "));
                        break;
                    case ".*":
                        valor = direccion.substring(0, checkSimbolIndex(direccion));
                        valores.add(valor);
                        direccion = direccion.substring(checkSimbolIndex(direccion));
                        break;
                    default:
                        valores.add(direccion);
                        break;
                }
            }
            else if (nextIsNumero(patron)) {
                patron = patron.substring(5);
                switch (checkNext(patron)) {
                    case "[,]":
                        valor = direccion.substring(0, direccion.indexOf(","));
                        valores.add(valor);
                        direccion = direccion.substring(direccion.indexOf(","));
                        break;
                    case "[ ]":
                        valor = direccion.substring(0, direccion.indexOf(" "));
                        valores.add(valor);
                        direccion = direccion.substring(direccion.indexOf(" "));
                        break;
                    case ".*":
                        valor = direccion.substring(0, checkSimbolIndex(direccion));
                        valores.add(valor);
                        direccion = direccion.substring(checkSimbolIndex(direccion));
                        break;
                    default:
                        valores.add(direccion);
                        break;
                }
            }
            else if (nextIsComa(patron)) {
                patron = patron.substring(3);
                direccion = direccion.substring(1);
            }
            else if (nextIsEspacio(patron)) {
                patron = patron.substring(3);
                direccion = direccion.substring(1);
            }
            else if (nextIsSimbolo(patron)) {
                patron = patron.substring(2);
                direccion = direccion.substring(1);
            }

            System.out.println("Valor: " + valor);
        }
    }
    public static int checkSimbolIndex(String direccion) {

        for (int i = 0; i < direccion.length(); i++) {
            if (!Character.isAlphabetic(direccion.charAt(i)) && !Character.isDigit(direccion.charAt(i)) && direccion.charAt(i) != ',' && direccion.charAt(i) != ' ')
                return i;
        }

        return 0;
    }

    public static String checkNext(String restoPatron) {

        if (nextIsLetras(restoPatron)) return "[A-Za-z]+";
        if (nextIsLetra(restoPatron)) return "[A-Za-z]";
        if (nextIsNumeros(restoPatron)) return "[0-9]+";
        if (nextIsNumero(restoPatron)) return "[0-9]";
        if (nextIsComa(restoPatron)) return "[,]";
        if (nextIsEspacio(restoPatron)) return "[ ]";
        if (nextIsSimbolo(restoPatron)) return ".*";

        return "";
    }

    public static boolean nextIsLetra(String patron) {
        try{
            if (patron.substring(0, 8).equals("[A-Za-z]"))
                return true;
        }catch (Exception e){
            return false;
        }
        return false;
    }
    public static boolean nextIsLetras(String patron) {
        try{
            if (patron.substring(0, 9).equals("[A-Za-z]+"))
                return true;
        }catch (Exception e){
            return false;
        }
        return false;
    }

    public static boolean nextIsNumero(String patron) {
        try{
            //System.out.println(patron.substring(0, 5));
            if (patron.substring(0, 5).equals("[0-9]"))
                return true;
        }catch (Exception e){
            return false;
        }
        return false;
    }
    public static boolean nextIsNumeros(String patron) {
        try{
            //System.out.println(patron.substring(0, 6));
            if (patron.substring(0, 6).equals("[0-9]+"))
                return true;
        }catch (Exception e){
            return false;
        }
        return false;
    }

    public static boolean nextIsComa(String patron) {
        try{
            //System.out.println(patron.substring(0, 3));
            if (patron.substring(0, 3).equals("[,]"))
                return true;
        }catch (Exception e){
            return false;
        }
        return false;
    }
    public static boolean nextIsEspacio(String patron) {
        try{
            //System.out.println(patron.substring(0, 3));
            if (patron.substring(0, 3).equals("[ ]"))
                return true;
        }catch (Exception e){
            return false;
        }
        return false;
    }
    public static boolean nextIsSimbolo(String patron) {
        try{
            //System.out.println(patron.substring(0, 2));
            if (patron.substring(0, 2).equals(".*"))
                return true;
        }catch (Exception e){
            return false;
        }
        return false;
    }

    public static void ordenarValores() {

        List<String> valoresOrganizados = new ArrayList<>();

        boolean contieneSimbolo;
        String valorActual = "";

        for (int i = 0; i < valores.size(); i++) {
            String valor = valores.get(i);
            if (valor.length() == 0)
                continue;
            contieneSimbolo = false;

            System.out.println("Valor: " + valor);

            for (int j = 0; j < valor.length(); j++)
                if (!Character.isAlphabetic(valor.charAt(j)) && !Character.isDigit(valor.charAt(j)) && valor.charAt(j) != ',' && valor.charAt(j) != ' ')
                    contieneSimbolo = true;

            if (contieneSimbolo)
                valoresOrganizados.add(valor);
            else {
                if (Character.isAlphabetic(valor.charAt(0)))
                    if (valorActual.length() > 0 && Character.isAlphabetic(valorActual.charAt(0)))
                        valorActual += " " + valor;
                    else valorActual += valor;
                else if (Character.isDigit(valor.charAt(0))) {
                    if (valorActual.length() > 0) valoresOrganizados.add(valorActual);
                    valorActual = "";
                    valoresOrganizados.add(valor);
                }
            }

            if (i == valores.size() - 1 && valorActual.length() > 0)
                valoresOrganizados.add(valorActual);
        }

        valores = valoresOrganizados;
    }
}
