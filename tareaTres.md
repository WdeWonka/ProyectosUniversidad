CODIGO : TAREA 3
     
    package unitOneShit;

COPIAR LIBRERIAS↓↓ 
    
    import java.util.Scanner;
    import java.util.Random;
    import java.util.Vector;


CODIGO ↓↓↓
  
    public static class listaProductos{
		  private Scanner teclado = new Scanner(System.in);
		  private Random  random = new Random();
		  private Vector<String> productos = new Vector<>();
		  private Vector<Double> precios = new Vector<>();
		  private int n ;
		
		    //CONSTRUCTOR
		    public listaProductos(int n) {
			  this.n = n;
			
			
		     for(int i = 0;i < n;i++) {
			      //LISTA DE PRODUCTOS
				    System.out.print("iNGRESE EL NOMBRE DEL PRODUCTO: ");
				    String nombreP = teclado.nextLine().trim();

				    // CONDiCiONALES EN CASO DE ERRORES TiPOGRAFiCOS
				    if (nombreP.isEmpty() || nombreP.matches(".*\\d+.*")) {
				    	 System.out.println("Error...");
				    	 i--;
				    	 if (!precios.isEmpty()) {
				             precios.remove(precios.size() - 1);
				         }
				    } else {
				    	productos.add(nombreP);
				    }

			 //PRECIOS DE PRODUCTO
			 double precioR = 25 + (200 -1) * random.nextDouble();
			 precioR = Math.round(precioR * 100.0) / 100.0;
			 precios.add(precioR);
			 
		 }
		
		 //ORDENAR PRODUCTOS VECTOR 
		 sortProductos();
		
		}
		
		private void sortProductos() {
			
			for(int i = 0; i < n - 1 ; i++) {
				for(int j = 0; j < n - i - 1;j++) {
					  String producto1 = productos.get(j);
			          String producto2 = productos.get(j + 1);
			         
			        //COMPARA LOS NOMBRES
			        if (producto1.compareToIgnoreCase(producto2) > 0) {
			        // CAMBiA DE LUGAR 
			         productos.set(j, producto2);
			         productos.set(j + 1, producto1);
			         
			        }
				}
			}
		}	    
		
	    public void printDatos() {
	        System.out.println("═══════════════════════════════════════");
	        System.out.println("LiSTA CON PRODUCTOS ORDENADOS ALFABETiCAMENTE: ");
	        
	        for (String producto : productos) {
	            System.out.println(producto.toLowerCase() + ": Q" + getPrecio(producto));
	        }
	        
	        System.out.println("");
	        System.out.println("═══════════════════════════════════════");
	        System.out.println("LiSTA CON PRECiOS EN ORDEN ASCENDENTE:");

         //ORDENA LOS NUMEROS DE MAYOR A MENOR
	        Vector<Double> sortedPrecios = new Vector<>(precios);
	        for (int i = 0; i < n - 1; i++) {
	            for (int j = 0; j < n - i - 1; j++) {
	                Double precio1 = sortedPrecios.get(j);
	                Double precio2 = sortedPrecios.get(j + 1);
	                
	                if (precio1 < precio2) {
	                    sortedPrecios.set(j, precio2);
	                    sortedPrecios.set(j + 1, precio1);
	                }
	            }
	        }
	        
	        for (Double precio : sortedPrecios) {
	            String producto = getProducto(precio);
	            System.out.println(producto.toLowerCase() + ": Q" + precio);
	        }
	    }
	    private Double getPrecio(String producto) {
	        int index = productos.indexOf(producto);
	        return precios.get(index);
	    }

	    private String getProducto(Double precio) {
	        int index = precios.indexOf(precio);
	        return productos.get(index);
	    }


		
		
	}
	
	
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner teclado = new Scanner(System.in);
		int n; 

		while (true) {
		    System.out.print("iNGRESE EL NUMERO DE PRODUCTOS: ");
		    
		    if (teclado.hasNextInt()) {
		        n = teclado.nextInt();
		        break;
		    } else {
		        System.out.println("Error...");
		        teclado.nextLine(); // C
		    }
		}
		
		listaProductos listaP = new listaProductos(n);
		listaP.printDatos();
		
	}



 

