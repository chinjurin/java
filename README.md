package excel;
import java.io.File;
import java.io.IOException;
import java.util.Scanner;
import jxl.Cell;
import jxl.Sheet;
import jxl.Workbook;
import jxl.read.biff.BiffException;
import jxl.write.Label;
import jxl.write.WritableSheet;
import jxl.write.WritableWorkbook;
import jxl.write.WriteException;
public class excel{
public static void createExcel() throws BiffException{
        try{
        Workbook wb = Workbook.getWorkbook(new File("C:\\Users\\akshara\\Desktop\\canteennew.xls"));
        WritableWorkbook copy = Workbook.createWorkbook(new File("cfile.xls"),wb);
        copy.createSheet("first sheet", 0);
        copy.write();
        copy.close();
        }catch(IOException | WriteException e){
        }
    }
    public static void writingExcel(){
    try{
        Workbook wb = Workbook.getWorkbook(new File("C:\\Users\\akshara\\Desktop\\canteennew.xls"));
        WritableWorkbook copy = Workbook.createWorkbook(new File("cfile.xls"),wb);
        WritableSheet copySheet = copy.getSheet(0);
        int row = copySheet.getRows();
        String itemname[] = new String[row];
        String itemprice[] = new String[row];
        String itemquan[] = new String[row];
        int opt;
        do{
        System.out.println("\n1.Enter new item\n2.Delete item\n3.Add number of available product\n4.Exit\n");
        System.out.println("Enter option: ");
        Scanner scan = new Scanner(System.in);
        opt = scan.nextInt();
        Scanner scan2 = new Scanner(System.in);
        Scanner scan3 = new Scanner(System.in);
        Scanner scan4 = new Scanner(System.in);
        switch(opt){
            case 1:
                System.out.println("Enter the number of items you would like to add to the list: ");
                int j = scan.nextInt();
                for(int i = 0;i<j;i++){
                    System.out.println("Enter the name of "+(i+1)+ " the item to add:");
                    itemname[i] = scan2.nextLine();
                    System.out.println("Enter it's price: ");
                    itemprice[i] = scan3.nextLine();
                    System.out.println("Enter the quantity available for sale: ");
                    itemquan[i] = scan4.nextLine();
                }
                for(int i = 0;i<j;i++){
                    int m = i+row;
                    String k = Integer.toString(m);
                    Label label = new Label(0,m,k);
                    copySheet.addCell(label);
                    Label label1 = new Label(1,m,itemname[i]);
                    copySheet.addCell(label1);
                    Label label2 = new Label(3,m,itemprice[i]);
                    copySheet.addCell(label2);
                    Label label3 = new Label(2,m,itemquan[i]);
                    copySheet.addCell(label3);
                }
                row = copySheet.getRows();
                break;
            case 2:
                System.out.println("Enter the item number for which you would like to delete: ");
                Scanner scan6 = new Scanner(System.in);
                int it1 = scan6.nextInt();
                for(int i = 0;i<4;i++){
                    Label lab = new Label(i,it1," ");
                    copySheet.addCell(lab);
                }
                for(int i = it1+1;i<row;i++){
                    for(int jl = 0;jl<1;jl++){
                       Cell m = copySheet.getCell(1,i);
                       itemname[i] = m.getContents();
                    }
                    for(int jl =0;jl<1;jl++){
                       Cell c = copySheet.getCell(2,i);
                       itemquan[i] = c.getContents();
                    }
                   for(int jl = 0;jl<1;jl++){
                       Cell k = copySheet.getCell(3,i);
                       itemprice[i] = k.getContents();
                   }
               }
                break;
            case 3:
                System.out.println("Enter the item number for which you would like to edit: ");
                Scanner scan5 = new Scanner(System.in);
                int it = scan5.nextInt();
                Cell jk = copySheet.getCell(1,it); 
                String anyone = jk.getContents();
                System.out.println("Enter the quantity change you would like to make for "+anyone+":");
                int m = scan5.nextInt();
                String k = Integer.toString(m);
                Label lab = new Label(2,it,k);
                copySheet.addCell(lab);
                break;
            case 4:
                System.out.println("\t\t\t\tTHANK YOU for using the ADMIN mode\n");
                break;
            default:
                break;
        }
        }while(opt!=4);
        copy.write();
        copy.close();
       
    }catch(IOException | IndexOutOfBoundsException | BiffException | WriteException e){
    }
    }
    public static void usermode() throws IOException, BiffException, WriteException{
        File file = new File("C:\\Users\\akshara\\Documents\\NetBeansProjects\\newcanteentest\\cfile.xls");
        int rows;
        Sheet s;
        if(!file.exists()){
            File f = new File("C:\\Users\\akshara\\Desktop\\canteennew.xls");
            Workbook wb = Workbook.getWorkbook(f);
            s = wb.getSheet(0);
        }else{
            Workbook wb = Workbook.getWorkbook(file);
            s = wb.getSheet(0);
        }
            rows = s.getRows();
            String[] names;
            names = new String[rows];
            String prices[];
            prices = new String[rows];
            String quantity[];
            quantity = new String[rows];
        for(int i = 1;i<rows;i++){
            for(int j = 0;j<1;j++){
                Cell m = s.getCell(1,i);
                names[i] = m.getContents();
            }
            for(int j =0;j<1;j++){
                Cell c = s.getCell(2,i);
                quantity[i] = c.getContents();
            }
            for(int j = 0;j<1;j++){
                Cell k = s.getCell(3,i);
                prices[i] = k.getContents();
            }
        }
        int ch;
        float total;
        total = (float) 0.0;
        int quan[];
        quan = new int[rows];
        float ft[];
        ft = new float[rows];
        int number[];
        number = new int[rows];
        String items[];
        items = new String[rows];
        int num = 0;
        int num1;
        int scan;
        int scan2;
        int jet = 0;
        for(int i = 0;i<rows;i++){
            ft[i] = 0;
        }
        Scanner sc1 = new Scanner(System.in);
        do{
        System.out.println("1.VIEW MENU\n2.PURCHASE\n3.STATEMENT\n4.EXIT\n");
        System.out.println("Enter your choice: ");
        ch = sc1.nextInt();
        switch(ch){
            case 1:
                System.out.println("\tMENU\n");
                for(int i=1;i<rows;i++){
                    System.out.println(i+". "+names[i]+" - "+quantity[i]+" nos - "+prices[i]+" Dhs\n");
                }
                break;
            case 2:
                if(ft[0]==0.0){
                System.out.println("Enter the number of items you would like to purchase: ");
                Scanner item = new Scanner(System.in);
                scan = item.nextInt();
                jet = jet + scan;
                for(int i = 0;i<scan;i++){                  
                    System.out.println("Enter the item number(for purchase): ");
                    Scanner buy = new Scanner(System.in);
                    num = buy.nextInt();
                    quan[i] = Integer.parseInt(quantity[num]);
                    System.out.println("Enter the Number of "+names[num]+" you would like to purchase: ");
                    int howmany;
                    howmany = buy.nextInt();
                    int mj = 1;
                    while(mj==1){
                    if( howmany <= quan[i] ){
                        ft[i] = Float.parseFloat(prices[num]);
                        items[i] = names[num];
                        number[i] = howmany;
                        int temp;
                        temp = quan[i];
                        temp -= howmany;
                        String tempor;
                        tempor = Integer.toString(temp);
                        quantity[num] = tempor;
                        total = (float)(total + (ft[i]*(howmany)));
                        mj = 0;
                    }else{
                        System.out.println("Sorry not enough available for purchase. Only "+quantity[num]+" available ");
                        System.out.println("Enter the number of "+names[num]+" you would like to purchase: ");
                        howmany = buy.nextInt();
                        mj = 1;
                    }
                    }
                }
                }else{
                    int j = 0;
                    while(ft[j]==0){
                        j++;
                    }
                    j++;
                    System.out.println("Enter the number of items you would like to purchase: ");
                    Scanner item1 = new Scanner(System.in);
                    scan2 = item1.nextInt();
                    jet = jet + scan2;
                    for(int i = j;i<=scan2;i++){
                    System.out.println("Enter the item number(for purchase): ");
                    Scanner buy2 = new Scanner(System.in);
                    num1 = buy2.nextInt();
                    ft[i] = Float.parseFloat(prices[num1]);
                    items[i] = names[num1];
                    quan[i] = Integer.parseInt(quantity[num1]);
                    System.out.println("Enter the Number of "+names[num1]+" you would like to purchase: ");
                    int howmany;
                    howmany = buy2.nextInt();
                    if( howmany <= quan[i] ){
                        number[i] = howmany;
                        int temp;
                        temp = Integer.parseInt(quantity[num1]);
                        temp -= howmany;
                        String tempor;
                        tempor = Integer.toString(temp);
                        quantity[num] = tempor;
                        total = (float) (total + (ft[i]*(howmany)));
                    }else{
                        System.out.println("Sorry not enough available for purchase. Only "+quantity[num1]+" available ");
                    }
                }
                }
            break;
            case 3:
                System.out.println("\t\tSTATEMENT\n");
                for(int i=0;i<jet;i++){
                    System.out.println((i+1)+". "+items[i]+" - "+number[i]+" nos - "+ft[i]+" Dhs\n");
                }
                System.out.println("The total is "+total+" Dhs\n");
                ch = 4;
                break;
            case 4:
                System.out.println("\t\t\t\t\t\tTHANK YOU!!!\n\t\t\t\t\t\tSEE YOU AGAIN\t");
                break;
            default:
                System.out.println("Enter correct option: ");
                break;
    }
    }while(ch!=4);
    }

}


