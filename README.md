# ProyectosUniversidad

PARCIAL I : CODIGO DEL PROYECTO FACTURA 

	package unitOneShit;

//COPIAR LAS LIBRERIAS  ↓↓↓↓

 	//LiBRERiAS DEL PROYECTO	
 	import java.text.SimpleDateFormat;
	import java.util.Date;
	import java.util.Random;
	import java.util.Scanner;
	

 //PARA LA PRUEBA DEL CODiGO COPiAR DESDE AQUi ↓↓↓

	public static class Productos{
		private int id;
		private String nombre;
		private double precio;
		private int cantidad;
	
		//CONSTRUCTOR 
		public Productos(int id, String nombre, double precio, int cantidad){
			this.id = id;
			this.nombre = nombre;
			this.precio = precio;
			this.cantidad = cantidad;
		}
		public int getId() {
			return id;
		}
		
		public String getNombre() {
			return nombre;
		}
		
		public double getPrecio() {
			return precio;
		}
		
		public int getCantidad() {
			return cantidad;
		}
	}
	
	public static class Hamburguesa extends Productos{ 
		public Hamburguesa(int cantidad) {
			super(01, "Hamburguesa", 45.00, cantidad);
		}
		public double calcularTotalHamburguesas() {
	        return getPrecio() * getCantidad();
	    }
	}
	
	public static class Papas extends Productos{
		public Papas(int cantidad) {
			super(02, "Papas Fritas", 25.00,cantidad);
		}
		
		public double calcularPapasTotal() {
			return getPrecio() * getCantidad();
		}
	}
	
	public static class Bebida extends Productos{
		public Bebida(int cantidad) {
			super(03,"CocaCola",9.00,cantidad);
		}
		
		public double calcularbebidaTotal() {
			return getPrecio() * getCantidad();
		}
	}
		
	public static class Factura{	
	private Scanner teclado;
	private String cliente;
	private String nit;
	private String metodoPago;
	private int nOrden;
	private String nombreH;
	private String nombreP;
	private String nombreB;
	//TOTALES GENERALES
	private double subtotal =0.0;
	private double iva =0.0;
	private double total= 0.0;
	
	//TOTAL DE LOS PRODUCTOS
	private double totalH = 0.0;
	private double totalP = 0.0;
	private double totalB = 0.0;
	private int cantidadH= 0;
	private int cantidadP= 0;
	private int cantidadB= 0;

	public String getFecha() {	
		Date fecha = new Date();
		SimpleDateFormat fechaformato = new SimpleDateFormat("dd-MM-YY hh:mm:ss");
		return fechaformato.format(fecha);
	}
	
	public  void menu() {
	teclado = new Scanner(System.in);
	
	String status = "";
	String confirmation= "";
	int cantidad = 0;
	do {
		System.out.println("╔══════════════════════════════════════╗");
		System.out.println("║           PROYECTO PARCIAL I         ║");
		System.out.println("║                 MENU                 ║");
		System.out.println("║  1.Hamburguesas      2.Papas Fritas  ║");
		System.out.println("║  3.CocaCola          4.Salir         ║");
		System.out.println("║                                      ║");
		System.out.println("║    WiLLiAM GARCiA | 0901-22-3022     ║");
		System.out.println("╚══════════════════════════════════════╝");
		
		System.out.print("¿Que Desea Ordenar? : ");
		String opcion = teclado.nextLine();
		
		switch(opcion) {
		
		case "1": 
			System.out.print("Cuantas hamburguesas desea ordenar?  →");
			  cantidad = teclado.nextInt();
			 teclado.nextLine();
			 Hamburguesa hamburguesa = new Hamburguesa(cantidad);
			 cantidadH += cantidad;
			 totalH += hamburguesa.calcularTotalHamburguesas();
			 
			 System.out.print("¿Desea ordenar algo más? (S/N): ");
				status = teclado.nextLine().toLowerCase();
			break;
			
		case "2":
			System.out.print("Cuantas porcines de papas desea ordenar?  → ");
			 cantidad = teclado.nextInt();
			teclado.nextLine();
			Papas papas = new Papas(cantidad);
			cantidadP += cantidad;
			totalP += papas.calcularPapasTotal();
			System.out.print("¿Desea ordenar algo más? (S/N): ");
			status = teclado.nextLine().toLowerCase();
			break;
			
		case "3":
			System.out.print("Cuantas bebidas desea ordenar?  → ");
			cantidad = teclado.nextInt();
			teclado.nextLine();
			Bebida bebida = new Bebida(cantidad);
			cantidadB += cantidad;
			totalB += bebida.calcularbebidaTotal();
			
			System.out.print("¿Desea ordenar algo más? (S/N): ");
 			status = teclado.nextLine().toLowerCase();
			break;
			
		case "4":
			System.out.print("Saliendo...");
			System.exit(0);
			
		default:
			System.out.println("ingrese una opcion valida!");
			confirmation = "n";
			break;
		}
		
		
		
		if(status.equals("n")) {  
 			System.out.print("Desea confirmar su orden y proceder al pago? (S/N) : ");
			confirmation = teclado.nextLine().toLowerCase();
		}
		if(status.equals("s")) {
			confirmation = "n";
		}
		
		
	}while(confirmation.equals("n")); 
	
	}

	public double calcSubtotal(){
		return subtotal = totalH + totalP + totalB;
	}
	
	public double calcIva() {
		return iva = subtotal * 0.12 ;
	}
	
	public double calcTotal() {
		return total = subtotal + iva;
	}
	
	public void pedirDatos() {
		teclado = new Scanner(System.in);
		//CREA UN NUMERO ALEATORiO
		Random rand = new Random();
		nOrden = rand.nextInt(9000) + 1000;
		subtotal = calcSubtotal();
		iva = calcIva();
		total = calcTotal();
		
		Hamburguesa hamburguesa = new Hamburguesa(cantidadH);
		nombreH = hamburguesa.getNombre();
		
		Papas papas = new Papas(cantidadP);
		nombreP = papas.getNombre();
		
		Bebida bebida = new Bebida(cantidadB);
		nombreB = bebida.getNombre();
		
		System.out.println("═══════════════════════════════");
		System.out.println("        Orden #" + nOrden);
   		System.out.println("-------------------------------");
		System.out.println("  Cant. " +          "Prod.       " +     "   Sub. " );
		if(cantidadH > 0) {
			System.out.println("   " + cantidadH + "    " + nombreH + "      " + totalH);
		}
		if(cantidadP > 0) {
			System.out.println("   " + cantidadP + "    " + nombreP + "      " + totalP);
		}
		if(cantidadB > 0) {
			System.out.println("   " + cantidadB + "    " + nombreB + "      " + totalB);
		}
    		System.out.println("-------------------------------");
		System.out.println("SUBTOTAL:         " + subtotal );
		System.out.println("IVA:              " + iva );
    		System.out.println("-------------------------------");
		System.out.println("TOTAL: Q          " + total );
    		System.out.println("-------------------------------");
		System.out.println("═══════════════════════════════");
		System.out.println("      DATOS DE FACTURACiON: ");
		System.out.println("ingrese su nombre y apellido: ");
		cliente = teclado.nextLine();
        	System.out.println("-------------------------------");
		System.out.println("Desea agregar nit para la factura? (S/N)");
		String a = teclado.nextLine().toLowerCase() ;
		if(a.equals("s")) {
			String confNit;
			do {
	            System.out.println("Ingrese el número de NIT:");
	            nit = teclado.nextLine();

	            System.out.println("¿Confirma el NIT ingresado? (s/n):");
	             confNit = teclado.nextLine().toLowerCase();

	        } while (!confNit.equalsIgnoreCase("s"));
		}else {
			nit = "C/F";
		}
    		System.out.println("-------------------------------");
		System.out.println("Metodo de pago: ");
		System.out.println("1.Efectivo: ");
		System.out.println("2.Tarjeta: ");
		System.out.println("Seleccione un metodo de pago (1/2): → ");
		String m = teclado.nextLine();
		
		if(m.equals("1")) {
			metodoPago = "Efectivo";
		}else if(m.equals("2")) {
			metodoPago = "Tarjeta";
		}
     
	}
	
	public void printFactura(){
		String fecha = getFecha();
		
    		System.out.println("");
    		System.out.println("imprimiendo factura....");
    		System.out.println("---------------------------------------");
    		System.out.println("");
    		System.out.println("");
		System.out.println("═══════════════════════════════════════");
		System.out.println("            Restaurante S.A          ");
		System.out.println("        Fecha & Hora de Emision:     ");
		System.out.println("          "+ fecha+"                 ");
		System.out.println("---------------------------------------");
		System.out.println("          Nombre:"+cliente+"     ");
		System.out.println("            NIT:"+nit+ "           ");
		System.out.println("---------------------------------------");
		System.out.println("           Orden #" + nOrden+"      ");
		System.out.println("---------------------------------------");
		System.out.println("     Cant. " +          "Prod.       " +     "    Sub. " );
		if(cantidadH > 0) {
			System.out.println("      " + cantidadH + "    " + nombreH + "  " + totalH);
		}
		if(cantidadP > 0) {
			System.out.println("      " + cantidadP + "    " + nombreP + "  " + totalP);
		}
		if(cantidadB > 0) {
			System.out.println("      " + cantidadB + "    " + nombreB + "  " + totalB);
		}
		System.out.println("---------------------------------------");
		System.out.println("     SUBTOTAL:             " + subtotal );
		System.out.println("     IVA:                  " + iva );
		System.out.println("---------------------------------------");
		System.out.println("     TOTAL: Q              " + total);
		System.out.println("---------------------------------------");
    		System.out.println("     PAGOS:");
    		System.out.println("     "+metodoPago + "             "+total);
		System.out.println("---------------------------------------");
    		System.out.println("                                     ");
    		System.out.println("         GRACIAS POR SU VISITA       ");
		System.out.println("═══════════════════════════════════════");	
	}
			
	}	
	    public static void main(String[] args) {
	       Factura factura = new Factura();
	       factura.menu();
		   factura.pedirDatos();
	       factura.printFactura(); 
	    }	

}


