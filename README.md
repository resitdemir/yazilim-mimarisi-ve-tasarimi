# yazilim-mimarisi-ve-tasarimi
## Behavioral(Davranışsal) Pattern
**Kalıp (Template ) Tasarım Deseni**

Template Metod tasarım deseni, behavioral tasarım desenlerinden biridir. 
Bir algoritmanın adımlarını tanımlamayı sağlar ve alt sınıfların bir veya daha fazla adımların implementasyonunu 
yapmasını olanak tanır. Örneğin, bir ev inşa etmek istiyoruz. 
Ev inşa etmek için şu adımlar gereklidir: bina temel atılması, bina sütunları, bina duvarları ve pencereler. 
Burada dikkat edilecek olan husus, adımların sırayla yapılmasının zorunlu olmasıdır. Pencereler takıldıktan sonra temel atılamaz,
önce temel atılır sonra bina sütunları yapılır, daha sonra duvarlar yapılır en son ise pencereler yapılır.
Template metod tasarımı ile bu adımların sırasıyla yapılması zorunlu hale getirilmiştir.

*Yararları:*<br>
Kodu tekrar kullanmak için çok yaygın bir tekniktir, bu sadece ana faydasıdır.

*Kullanımı:*<br>
Alt sınıflar arasındaki ortak davranışın, tekrardan kaçınarak tek bir ortak sınıfa taşınması gerektiğinde kullanılır.

*Class diagramı:*<br>
![Class diagrami](https://github.com/resitdemir/yazilim-mimarisi-ve-tasarimi/blob/master/Template_PatternDiagram.png)

*Aşama 1:*<br>
Bir Oyun soyut sınıfı oluşturun.Buradaki abstract sınıfımızda metot gövdelerini tanımlıyoruz.

public abstract class Game {  
      
       abstract void initialize();  
       abstract void start();  
       abstract void end();  
      
       public final void play(){  
  
          //initialize the game  
          initialize();  
  
          //start game  
          start();  
            
          //end game  
          end();  
       }  }
       
       
*Aşama 2:*<br>
Yöntemine tanım vermek için Game abstract sınıfını genişletecek bir Chess sınıfı oluşturun.
Miras aldığımız Game sınıfının metotlarını Override ediyoruz.Yapımıza göre kodlarımızı yazıyoruz.
Burada kullanıcıya oyun hakkında üç aşamada bilgi veriyoruz.

public class Chess extends Game {  

     @Override  
       void initialize() {  
          System.out.println("Chess Game Initialized! Start playing.");  
       }  
     @Override  
       void start() {  
          System.out.println("Game Started. Welcome to in the chess game!");  
       }  
    @Override  
       void end() {  
          System.out.println("Game Finished!");  
       }  
}

*Aşama 3:*<br>
Yöntemine tanım vermek için Game abstract sınıfını genişletecek bir Soccer sınıfı oluşturun .
Aşama ikide yaptığımız işlemleri aynı şekilde Soccer sınıfı içinde uyarlıyoruz.

public class Soccer extends Game {  
      
    @Override  
       void initialize() {  
          System.out.println("Soccer Game Initialized! Start playing.");  
       }  
  
    @Override  
       void start() {  
          System.out.println("Game Started. Welcome to in the Soccer game!");  
       }  
         
    @Override  
       void end() {  
          System.out.println("Game Finished!");  
       }  
}

*Aşama 4:*<br>
Bir TemplatePatternDemo sınıfı oluşturun .
Main' de Game classının nesnesini oluşturuyoruz.

public class TemplatePatternDemo {  
public static void main(String[] args) throws InstantiationException, IllegalAccessException, ClassNotFoundException {

         Class c=Class.forName(args[0]);  
         Game game=(Game) c.newInstance();   //'c' tipinde bir nesne oluşturuldu. 
         game.play();   //Çıktıları ekrana yazdırıyoruz.    
       }  
}

## Creational(Yaratımsal) Pattern

**Kopya Nesne ( Prototype ) Tasarım Deseni**

Prototype (prototip) tasarım deseni creational grubununa ait, var olan nesnelerin kopyasının üretiminden sorumlu tasarım desenidir.
nesnelerin üretim maliyetini azaltmak için var olan nesnenin kopyasının üretilmesi yoluna gidilebilinir.
Prototype tasarım deseni böyle durumdaki nesnelerin yönetilmesini sağlar. Buradaki kopyalama işlemi “Deep Copy – Derin Kopyalama” şeklindedir, 
yani nesne bire bir kopyalanarak yeni referans değerlere atanır.  Prototype tasarım deseni uygulanması oldukça basittir. İlk olarak içinde kendi
türünde değer döndüren bir metot tanımlanmış olan interface veya abstract sınıf tanımlıyoruz. Çalışma zamanında kopyası alınabilecek nesnelerde
bu interface veya abstract sınıfı uyguluyoruz. 

*Yararları:*<br>
Alt sınıflandırma ihtiyacını azaltır.
Nesne oluşturmanın karmaşıklıklarını gizler.
İstemciler, ne tür bir nesne olacağını bilmeden yeni nesneler alabilir.
Çalışma zamanında nesne eklemenizi veya kaldırmanızı sağlar.

*Kullanımı:*<br>
Sınıflar çalışma zamanında başlatıldığında.
Bir nesne yaratmanın maliyeti pahalı veya karmaşık olduğunda.
Sınıf sayısını bir uygulamada minimum tutmak istediğinizde.
İstemci uygulamasının nesne oluşturma ve temsilinden habersiz olması gerektiğinde.

*Class Diagram:*<br>
![Class Diagram](https://github.com/resitdemir/yazilim-mimarisi-ve-tasarimi/blob/master/Prototype_Design_PatternDiagram.PNG)

- Prototype tipinde bir interface oluşturuyoruz , Prototype tipinde bir getClone() methodu oluşturuyoruz.
- Ardından, EmployeeRecord nesnesinin klonlanmasını sağlayan Prototip arabirimini uygulayan somut bir sınıf EmployeeRecord oluşturuyoruz .
- PrototypeDemo sınıfı bu somut sınıf EmployeeRecord'u kullanacaktır .



Prototip tasarım modeli örneğine bakalım.

Dosya: Prototype.java

interface Prototype {

     public Prototype getClone();      
}

Dosya:EmployeeRecord.java

class EmployeeRecord implements Prototype{  
      
   private int id;  
   private String name, designation;  
   private double salary;  
   private String address;  
      
   public EmployeeRecord(){  
            System.out.println("   Employee Records of Oracle Corporation ");  
            System.out.println("---------------------------------------------");  
            System.out.println("Eid"+"\t"+"Ename"+"\t"+"Edesignation"+"\t"+"Esalary"+"\t\t"+"Eaddress");  
      
}  
  
 public  EmployeeRecord(int id, String name, String designation, double salary, String address) {  
          
        this();  
        this.id = id;  
        this.name = name;  
        this.designation = designation;  
        this.salary = salary;  
        this.address = address;  
    }  
      
  public void showRecord(){  
          
        System.out.println(id+"\t"+name+"\t"+designation+"\t"+salary+"\t"+address);  
   }  
  
    @Override  
    public Prototype getClone() {  
          
        return new EmployeeRecord(id,name,designation,salary,address);  
    }  
}

Dosya: PrototypeDemo.java

import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
  
class PrototypeDemo{  
     public static void main(String[] args) throws IOException {  
          
        BufferedReader br =new BufferedReader(new InputStreamReader(System.in));  
        System.out.print("Enter Employee Id: ");  
        int eid=Integer.parseInt(br.readLine());  
        System.out.print("\n");  
          
        System.out.print("Enter Employee Name: ");  
        String ename=br.readLine();  
        System.out.print("\n");  
          
        System.out.print("Enter Employee Designation: ");  
        String edesignation=br.readLine();  
        System.out.print("\n");  
          
        System.out.print("Enter Employee Address: ");  
        String eaddress=br.readLine();  
        System.out.print("\n");  
          
        System.out.print("Enter Employee Salary: ");  
        double esalary= Double.parseDouble(br.readLine());  
        System.out.print("\n");  
           
        EmployeeRecord e1=new EmployeeRecord(eid,ename,edesignation,esalary,eaddress);  
          
        e1.showRecord();  
        System.out.println("\n");  
        EmployeeRecord e2=(EmployeeRecord) e1.getClone();  
        e2.showRecord();  
    }     
}

## Kaynakça:<br>
[https://www.javatpoint.com/design-patterns-in-java](https://www.javatpoint.com/design-patterns-in-java)  

[https://www.codesenior.com/tutorial/Template-Metod-Tasarim-Deseni](https://www.codesenior.com/tutorial/Template-Metod-Tasarim-Deseni)

[http://harunozer.com/makale/prototype_tasarim_deseni__prototype_design_pattern.htm](http://harunozer.com/makale/prototype_tasarim_deseni__prototype_design_pattern.htm)

