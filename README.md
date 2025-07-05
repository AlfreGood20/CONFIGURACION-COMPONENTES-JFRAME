# CONFIGURACION-COMPONENTES-JFRAME
En este README se encuentra una clase de java, donde se puede usar para JFrame en este se encuentran metodos mas usandos de componentes y ayuda a disminuir el tiempo de desarrollo.

```java
import java.awt.Color;
import java.awt.Cursor;
import java.awt.Font;
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
import javax.imageio.ImageIO;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JCheckBox;
import javax.swing.JLabel;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JRadioButton;
import javax.swing.JTable;
import javax.swing.JTextField;
import javax.swing.border.EmptyBorder;

public class ConfiguracionVistas { 

	public static JLabel etiquetas(String nombre, int x, int y, int ancho, int altura, Color colorEtiqueta,int tamañoLetra, String tipoDeEstilo) {
		JLabel etiqueta = new JLabel(nombre);
		etiqueta.setBounds(x, y, ancho, altura);
		etiqueta.setForeground(colorEtiqueta);
		etiqueta.setFont(new Font(tipoDeEstilo, Font.BOLD, tamañoLetra));
		return etiqueta;
	}

	public static JTextField campos(int x, int y, int ancho, int altura, String tipoLetra, int tamañoLetra) {
		JTextField campo = new JTextField();
		campo.setBounds(x, y, ancho, altura);
		campo.setFont(new Font(tipoLetra, Font.BOLD, tamañoLetra));
		return campo;
	}
	
	public static JButton button(String nombre,int x, int y, int ancho, int altura,Color colorBoton) {
		JButton boton=new JButton(nombre);
		boton.setBounds(x, y, ancho, altura);
		boton.setBackground(colorBoton);
		boton.setCursor(new Cursor(Cursor.HAND_CURSOR)); //PONE EL LA MANITO DEL PUNTERO DEL MAUSE
		return boton;
	}
	
	public static JMenu menu(String nombre, int arriba, int izquierda,int abajo, int derecha,Color color,int tamañoLetra, String tipoDeEstilo) {
		JMenu menu=new JMenu(nombre);
		menu.setBorder(new EmptyBorder(arriba,izquierda,abajo,derecha));
		menu.setFont(new Font(tipoDeEstilo, Font.BOLD, tamañoLetra));
		menu.setForeground(color);
		return menu;
	}
	
	public static JMenuItem item(String nombre, int arriba, int izquierda,int abajo, int derecha,Color color,int tamañoLetra, String tipoDeEstilo) {
		JMenuItem item=new JMenuItem(nombre);
		item.setBorder(new EmptyBorder(arriba,izquierda,abajo,derecha));
		item.setFont(new Font(tipoDeEstilo,Font.BOLD,tamañoLetra));
		item.setForeground(color);
		return item;
	}
	
	public static JCheckBox checkBox(String nombre, int x,int y, int ancho, int altura,Color colorLetras,int tamañoLetra, String tipoDeEstilo){
		JCheckBox cuadrito=new JCheckBox(nombre);
		cuadrito.setBounds(x, y, ancho,altura);
		cuadrito.setForeground(colorLetras);
		cuadrito.setFont(new Font(tipoDeEstilo,Font.BOLD,tamañoLetra));
		return cuadrito;
	}
	
	public static JRadioButton radioBoton(String nombre,int x,int y,int ancho,int altura,Color colorLetras,int tamañoLetra, String tipoDeEstilo) {
		JRadioButton button=new JRadioButton(nombre);
		button.setBounds(x, y, ancho, altura);
		button.setForeground(colorLetras);
		button.setFont(new Font(tipoDeEstilo,Font.BOLD,tamañoLetra));
		return button;
	}
	
	public static JTable tabla(String [] columnas,Object [][] datos,Color colorLetras,Color colorFondoCuadro,int tamañoLetra, String tipoDeEstiloColumnas,int tamañoFila,String tipoDeEstiloDatos,int tamañoLetraDatos) {
		JTable tabla = new JTable(datos, columnas);
		
		tabla.getTableHeader().setFont(new Font(tipoDeEstiloColumnas, Font.BOLD, tamañoLetra));
		tabla.getTableHeader().setBackground(colorFondoCuadro);
		tabla.getTableHeader().setForeground(colorLetras);
		
		tabla.setFont(new Font(tipoDeEstiloDatos, Font.BOLD, tamañoLetraDatos));
		tabla.setRowHeight(tamañoFila);
		
		return tabla;
	}

	// METODO SUELTO PARA PODER ELIMINAR EL TEXTO DE CORREO O CONTRASEÑA
	public static void addPlaceholder(JTextField textField, String placeholder) {
		textField.setText(placeholder);
		textField.setForeground(Color.GRAY); // Color inicial para el texto del placeholder

		textField.addFocusListener(new java.awt.event.FocusAdapter() {
			@Override
			public void focusGained(java.awt.event.FocusEvent e) {
				if (textField.getText().equals(placeholder)) {
					textField.setText(""); // Elimina el placeholder al ganar foco
					textField.setForeground(Color.BLACK); // Cambia el color del texto
				}
			}

			@Override
			public void focusLost(java.awt.event.FocusEvent e) {
				if (textField.getText().isEmpty()) {
					textField.setText(placeholder); // Restaura el placeholder si está vacío
					textField.setForeground(Color.GRAY); // Cambia el color al placeholder
				}
			}
		});
	}
	
	public static JLabel imagenEtiqueta(String url, int x, int y, int ancho, int altura) {
	    try {
	        //CREAMOS LA IMAGEN CON LA FUNCION DEL SISTEMA
	        BufferedImage imagenOriginal = ImageIO.read(new File(url));

	        //IMAGEN ESCALADA
	        Image imagenEscalada = imagenOriginal.getScaledInstance(ancho, altura, Image.SCALE_FAST); // Más rápido que SCALE_SMOOTH

	        //ESTO DIBUJA LA IMAGEN PARA QUE SEA MAS RAPIDO
	        BufferedImage imagenFinal = new BufferedImage(ancho, altura, BufferedImage.TYPE_INT_ARGB);
	        Graphics2D g2d = imagenFinal.createGraphics();
	        g2d.drawImage(imagenEscalada, 0, 0, null);
	        g2d.dispose();
	        
	        //SE LO AGREGAMOS A LA ETIQUETA
	        JLabel ilustracion = new JLabel(new ImageIcon(imagenFinal));
	        ilustracion.setBounds(x, y, ancho, altura);
	        return ilustracion;
	        
	    } catch (IOException e) {
	        e.printStackTrace();
	        return new JLabel("Error al cargar imagen");
	    }
	}
}
´´´´
