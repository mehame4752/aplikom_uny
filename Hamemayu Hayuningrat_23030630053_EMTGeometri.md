# Visualisasi dan Perhitungan Geometri dengan EMT
Euler menyediakan beberapa fungsi untuk melakukan visualisasi dan perhitungan geometri, baik
secara numerik maupun analitik (seperti biasanya tentunya, menggunakan Maxima).
Fungsi-fungsi untuk visualisasi dan perhitungan geometeri tersebut disimpan di dalam file
program "geometry.e", sehingga file tersebut harus dipanggil sebelum menggunakan
fungsi-fungsi atau perintah-perintah untuk geometri.


\>load geometry


    Numerical and symbolic geometry.

## Fungsi-fungsi Geometri

Fungsi-fungsi untuk Menggambar Objek Geometri:


  defaultd:=textheight()*1.5: nilai asli untuk parameter d  
  setPlotrange(x1,x2,y1,y2): menentukan rentang x dan y pada bidang koordinat  
  setPlotRange(r): pusat bidang koordinat (0,0) dan batas-batas sumbu-x dan y adalah -r sd r  
  plotPoint (P, "P"): menggambar titik P dan diberi label "P"  
  plotSegment (A,B, "AB", d): menggambar ruas garis AB, diberi label "AB" sejauh d  
  plotLine (g, "g", d): menggambar garis g diberi label "g" sejauh d  
  plotCircle (c,"c",v,d): Menggambar lingkaran c dan diberi label "c"  
  plotLabel (label, P, V, d): menuliskan label pada posisi P  

Fungsi-fungsi Geometri Analitik (numerik maupun simbolik):


  turn(v, phi): memutar vektor v sejauh phi  
  turnLeft(v):   memutar vektor v ke kiri  
  turnRight(v):  memutar vektor v ke kanan  
  normalize(v): normal vektor v  
  crossProduct(v, w): hasil kali silang vektorv dan w.  
  lineThrough(A, B): garis melalui A dan B, hasilnya [a,b,c] sdh. ax+by=c.  
  lineWithDirection(A,v): garis melalui A searah vektor v  
  getLineDirection(g): vektor arah (gradien) garis g  
  getNormal(g): vektor normal (tegak lurus) garis g  
  getPointOnLine(g):  titik pada garis g  
  perpendicular(A, g):  garis melalui A tegak lurus garis g  
  parallel (A, g):  garis melalui A sejajar garis g  
  lineIntersection(g, h):  titik potong garis g dan h  
  projectToLine(A, g):   proyeksi titik A pada garis g  
  distance(A, B):  jarak titik A dan B  
  distanceSquared(A, B):  kuadrat jarak A dan B  
  quadrance(A, B): kuadrat jarak A dan B  
  areaTriangle(A, B, C):  luas segitiga ABC  
  computeAngle(A, B, C):   besar sudut &lt;ABC  
  angleBisector(A, B, C): garis bagi sudut &lt;ABC  
  circleWithCenter (A, r): lingkaran dengan pusat A dan jari-jari r  
  getCircleCenter(c):  pusat lingkaran c  
  getCircleRadius(c):  jari-jari lingkaran c  
  circleThrough(A,B,C):  lingkaran melalui A, B, C  
  middlePerpendicular(A, B): titik tengah AB  
  lineCircleIntersections(g, c): titik potong garis g dan lingkran c  
  circleCircleIntersections (c1, c2):  titik potong lingkaran c1 dan c2  
  planeThrough(A, B, C):  bidang melalui titik A, B, C  

Fungsi-fungsi Khusus Untuk Geometri Simbolik:


  getLineEquation (g,x,y): persamaan garis g dinyatakan dalam x dan y  
  getHesseForm (g,x,y,A): bentuk Hesse garis g dinyatakan dalam x dan y dengan titik A pada  
  sisi positif (kanan/atas) garis  
  quad(A,B): kuadrat jarak AB  
  spread(a,b,c): Spread segitiga dengan panjang sisi-sisi a,b,c, yakni sin(alpha)^2 dengan  
  alpha sudut yang menghadap sisi a.  
  crosslaw(a,b,c,sa): persamaan 3 quads dan 1 spread pada segitiga dengan panjang sisi a, b, c.  
  triplespread(sa,sb,sc): persamaan 3 spread sa,sb,sc yang memebntuk suatu segitiga  
  doublespread(sa): Spread sudut rangkap Spread 2*phi, dengan sa=sin(phi)^2 spread a.  

## Contoh 1: Luas, Lingkaran Luar, Lingkaran Dalam Segitiga

Untuk menggambar objek-objek geometri, langkah pertama adalah menentukan rentang sumbu-sumbu
koordinat. Semua objek geometri akan digambar pada satu bidang koordinat, sampai didefinisikan
bidang koordinat yang baru.


\>setPlotRange(-0.5,2.5,-0.5,2.5); // mendefinisikan bidang koordinat baru 

\>function f(x)


Sekarang atur ketiga titik dan plotkan


\>A=[1,0]; plotPoint(A,"A"); // definisi dan gambar tiga titik

\>B=[0,1]; plotPoint(B,"B");

\>C=[2,2]; plotPoint(C,"C");


Lalu tiga segmen


\>plotSegment(A,B,"c"); // c=AB

\>plotSegment(B,C,"a"); // a=BC

\>plotSegment(A,C,"b"); // b=AC


Fungsi geometri termasuk kedalam fungsi untuk membuat garis dan lingkaran. Format untuk garis adalah [a, b, c]
yang mana merepresentasikan garis dengan persamaan ax+by = c.


\>lineBC = lineThrough(B,C);

\>lineAB = lineThrough(A,B);

\>lineAC = lineThrough(A,C);

\>lineBC // garis yang melalui B dan C


    [-1,  2,  2]

Menghitung garis singgung melalui A dalam BC.


\>h=perpendicular(A,lineThrough(B,C)); // garis h tegak lurus BC melalui A


dan titik potong dengan BC.


\>D=lineIntersection(h,lineThrough(B,C)); // D adalah titik potong h dan BC


Buat plotnya.


\>plotPoint(D,value=1); // koordinat D ditampilkan

\>aspect(1); plotSegment(A,D): // tampilkan semua gambar hasil plot...()


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-001.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-001.png)

Hitung luas ABC:


\>norm(A-D)\*norm(B-C)/2 // AD=norm(A-D), BC=norm(B-C)


    1.5

Bandingkan dengan formula determinan.


\>areaTriangle(A,B,C) // hitung luas segitiga langusng dengan fungsi


    1.5

Cara lain menghitung luas segitiga ABC:


\>distance(A,D)\*distance(B,C)/2


    1.5

Sudut pada C.


\>degprint(computeAngle(B,C,A))


    36°52'11.63''

Sekarang keliling lingkaran dari segitiga


\>c=circleThrough(A,B,C); // lingkaran luar segitiga ABC

\>R=getCircleRadius(c); // jari2 lingkaran luar 

\>O=getCircleCenter(c); // titik pusat lingkaran c 

\>plotPoint(O,"O"); // gambar titik "O"

\>plotCircle(c,"Lingkaran luar segitiga ABC"):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-002.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-002.png)

Tampilkan koordinat titik pusat dan jari-jari lingkaran luar.


\>O, R


    [1.16667,  1.16667]
    1.17851130198

Sekarang akan digambar lingkaran dalam segitiga ABC. Titik pusat lingkaran dalam adalah
titik potong garis-garis bagi sudut.


\>l=angleBisector(A,C,B); // garis bagi <ACB

\>g=angleBisector(C,A,B); // garis bagi <CAB

\>P=lineIntersection(l,g) // titik potong kedua garis bagi sudut


    [0.86038,  0.86038]

dan plotkan semuanya.


\>color(5); plotLine(l); plotLine(g); color(1); // gambar kedua garis bagi sudut

\>plotPoint(P,"P"); // gambar titik potongnya

\>r=norm(P-projectToLine(P,lineThrough(A,B))) // jari-jari lingkaran dalam


    0.509653732104

\>circleInside=circleWithCenter(P,r);

\>plotCircle(circleInside, "Lingkaran dalam segitiga ABC"): // gambar lingkaran dalam


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-003.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-003.png)

## Latihan

1. Tentukan ketiga titik singgung lingkaran dalam dengan sisi-sisi segitiga ABC.


2. Gambar segitiga dengan titik-titik sudut ketiga titik singgung tersebut. Merupakan segitiga apakah itu?


3. Hitung luas segitiga tersebut.


4. Tunjukkan bahwa garis bagi sudut yang ke tiga juga melalui titik pusat lingkaran dalam.


5. Gambar jari-jari lingkaran dalam.


6. Hitung luas lingkaran luar dan luas lingkaran dalam segitiga ABC. Adakah hubungan antara luas kedua lingkaran
tersebut dengan luas segitiga ABC?


1. Akan ditentukan Ketiga titik singgung lingkaran dalam dengan sisi-sisi segitiga ABC


\>E = lineCircleIntersections(lineAB, circleInside) // intersection line with line AB


    [0.5,  0.5]

\>F = lineCircleIntersections(lineAC, circleInside) // intersection line with line AC


    [1.31623,  0.632456]

\>G = lineCircleIntersections(lineBC, circleInside) // intersection line with line BC


    [0.632456,  1.31623]

Jadi titik singgung lingkaran dalam dengan sisi-sisi segitiga AB adalah


Untuk titik singgung lingkaran dalam dengan ruas garis AB adalah


Untuk titik singgung lingkaran dalam dengan ruas garis AC adalah


Untuk titik singgung lingkaran dalam dengan ruas garis BC adalah


2. Akan digambar segitiga dengan titik-titik sudut ketiga titik singgung tersebut. dan akan ditentukan jenis
segitiganya.


Pertama-tama buat titik


\>plotPoint(E, "E");

\>plotPoint(F, "F");

\>plotPoint(G, "G");


Kemudian buat segmennya


\>plotSegment(E, F, "g"); // g = EF

\>plotSegment(E, G, "f"); // f = EG

\>plotSegment(F, G, "e"): // e = FG


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-004.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-004.png)

\>distanceEF = distance(E, F);

\>distanceEG = distance(E, G);

\>distanceFG = distance(F, G);

\>distanceEF


    0.826905214631

\>distanceEG


    0.826905214631

\>distanceFG


    0.966999966873

Karena ruas garis EF dan EG sama, akan tetapi ruas garis FG berbeda dengan ketiganya, maka segitiga ini termasuk
kedalam segitiga sama kaki.


3. Akan dihitung luas segitiga tersebut


dapat dengan mudah dengan fungsi areaTriangle


\>areaTriangle(E, F, G)


    0.324341649025

Diperoleh luas segitiga sekitar




dengan satuan luas


4. Akan ditunjukkan garis bagi sudut yang ketiga melalui titik pusat lingkaran dalam


\>h = angleBisector(C, B, A); // garis bagi <CBA

\>color(5); plotLine(h):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-005.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-005.png)

Terlihat bahwa garis bagi untuk CBA akan melalui titik pusat lingkaran dalam


\>S = lineIntersection(l, h);

\>T = lineIntersection(g, h);

\>S


    [0.86038,  0.86038]

\>T


    [0.86038,  0.86038]

\>P


    [0.86038,  0.86038]

Lebih lanjut dibuktikan bahwa titik potong untuk garis dengan titik sudut CBA akan melalui titik pusat lingkaran
dalam dimana titik potongnya


untuk titik potong garis bagi CBA dengan garis bagi ACB pada titik


untuk titik potong garis bagi CBA dengan garis bagi CAB pada titik


dengan titik pusat lingkaran dalamnya adalah


Sehingga, garis bagi untuk CBA akan melalui titik pusat lingkaran dalam


5. Akan digambar jari-jari lingkaran dalam


Dengan mudah dapat digambarkan antara titik PG, PF, atau PE


\>color(4); plotSegment(P, G, "PG"); plotSegment(P, F, "PF"); plotSegment(P, E, "PE"); color(1):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-006.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-006.png)

6. Akan dihitung luas lingkaran luar dan luas lingkaran dalam segitiga ABC. Akan ditentukan hubungannya.


\>areaCircleOutside = pi \* R^2;

\>areaCircleInside = pi \* r^2;

\>areaCircleOutside


    4.36332312999

\>areaCircleInside


    0.81601903655

Hubungan yang didapatkan adalah


- Jari-jari lingkaran luar lebih panjang daripada jari-jari lingkaran dalam segitiga, sehingga luasnya juga
demikian


# Contoh 2: Geometri Smbolik

Kita dapat menghitung dengan tepat dan geometri simbolik menggunakan Maxima.


File geometry.e menyediakan fungsi-fungsi yang sama (dan lebih) dalam Maxima. Namun. kita sekarang dapat
menggunakan perhitungan simbolik.


\>A &= [1,0]; B &= [0,1]; C &= [2,2]; // menentukan tiga titik A, B, C


Fungsi-fungsi untuk garis dan lingkaran bekerja seperti fungsi-fungsi Euler, tetapi menyediakan kompoutasi
simbolik.


\>c &= lineThrough(B,C) // c=BC


    
                                 [- 1, 2, 2]
    

Kita dapat mendapatkan persamaan untuk sebuah garis dengan mudah.


\>$getLineEquation(c,x,y), $solve(%,y) | expand // persamaan garis c


$$\left[ y=\frac{x}{2}+1 \right] $$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-008.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-008.png)

\>$getLineEquation(lineThrough([x1,y1],[x2,y2]),x,y), $solve(%,y) // persamaan garis melalui(x1, y1) dan (x2, y2)


$$\left[ y=\frac{-\left({\it x_1}-x\right)\,{\it y_2}-\left(x-  {\it x_2}\right)\,{\it y_1}}{{\it x_2}-{\it x_1}} \right] $$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-010.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-010.png)

\>$getLineEquation(lineThrough(A,[x1,y1]),x,y) // persamaan garis melalui A dan (x1, y1)


$$\left({\it x_1}-1\right)\,y-x\,{\it y_1}=-{\it y_1}$$\>h &= perpendicular(A,lineThrough(B,C)) // h melalui A tegak lurus BC


    
                                  [2, 1, 2]
    

\>Q &= lineIntersection(c,h) // Q titik potong garis c=BC dan h


    
                                     2  6
                                    [-, -]
                                     5  5
    

\>$projectToLine(A,lineThrough(B,C)) // proyeksi A pada BC


$$\left[ \frac{2}{5} , \frac{6}{5} \right] $$\>$distance(A,Q) // jarak AQ


$$\frac{3}{\sqrt{5}}$$\>cc &= circleThrough(A,B,C); $cc // (titik pusat dan jari-jari) lingkaran melalui A, B, C


$$\left[ \frac{7}{6} , \frac{7}{6} , \frac{5}{3\,\sqrt{2}} \right] $$\>r&=getCircleRadius(cc); $r , $float(r) // tampilkan nilai jari-jari


$$1.178511301977579$$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-016.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-016.png)

\>$computeAngle(A,C,B) // nilai <ACB


$$\arccos \left(\frac{4}{5}\right)$$\>$solve(getLineEquation(angleBisector(A,C,B),x,y),y)[1] // persamaan garis bagi <ACB


$$y=x$$\>P &= lineIntersection(angleBisector(A,C,B),angleBisector(C,B,A)); $P // titik potong 2 garis bagi sudut


$$\left[ \frac{\sqrt{2}\,\sqrt{5}+2}{6} , \frac{\sqrt{2}\,\sqrt{5}+2  }{6} \right] $$\>P() // hasilnya sama dengan perhitungan sebelumnya


    [0.86038,  0.86038]

## Perpotongan Garis dan Lingkaran

Tentu saja, kita juga dapat membuat perpotongan garis dengan lingkaran, dan lingkaran dengan lingkaran.


\>A &:= [1,0]; c=circleWithCenter(A,4);

\>B &:= [1,2]; C &:= [2,1]; l=lineThrough(B,C);

\>setPlotRange(5); plotCircle(c); plotLine(l);


Perpotongan garis dengan lingkaran mengembalikan dua titik dan jumlah titik yang berpotongan


\>{P1,P2,f}=lineCircleIntersections(l,c);

\>P1, P2, f


    [4.64575,  -1.64575]
    [-0.645751,  3.64575]
    2

\>plotPoint(P1); plotPoint(P2):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-020.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-020.png)

Sama dalam Maxima.


\>c &= circleWithCenter(A,4) // lingkaran dengan pusat A jari-jari 4


    
                                  [1, 0, 4]
    

\>l &= lineThrough(B,C) // garis l melalui B dan C


    
                                  [1, 1, 3]
    

\>$lineCircleIntersections(l,c) | radcan, // titik potong lingkaran c dan garis l


$$\left[ \left[ \sqrt{7}+2 , 1-\sqrt{7} \right]  , \left[ 2-\sqrt{7}   , \sqrt{7}+1 \right]  \right] $$Akan ditunjukkan bahwa sudut-sudut yang menghadap busur yang sama adalah sama besar.


\>C=A+normalize([-2,-3])\*4; plotPoint(C); plotSegment(P1,C); plotSegment(P2,C);

\>degprint(computeAngle(P1,C,P2))


    69°17'42.68''

\>C=A+normalize([-4,-3])\*4; plotPoint(C); plotSegment(P1,C); plotSegment(P2,C);

\>degprint(computeAngle(P1,C,P2))


    69°17'42.68''

\>insimg;


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-022.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-022.png)

## Garis Sumbu

Berikut adalah langkah-langkah menggambar garis sumbu ruas garis AB:


1. Gambar lingkaran dengan pusat A melalui B.


2. Gambar lingkaran dengan pusat B melalui A.


3. Tarik garis melalui kedua titik potong kedua lingkaran tersebut. Garis ini merupakan garis sumbu (melalui
titik tengah dan tegak lurus) AB.


\>A=[2,2]; B=[-1,-2];

\>c1=circleWithCenter(A,distance(A,B));

\>c2=circleWithCenter(B,distance(A,B));

\>{P1,P2,f}=circleCircleIntersections(c1,c2);

\>l=lineThrough(P1,P2);

\>setPlotRange(-10, 10, -10, 10); plotCircle(c1); plotCircle(c2);

\>plotPoint(A); plotPoint(B); plotSegment(A,B); plotLine(l):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-023.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-023.png)

Selanjutnya, kami lakukan yang sama pada Maxima dengan koordinat umum.


\>A &= [a1,a2]; B &= [b1,b2];

\>c1 &= circleWithCenter(A,distance(A,B));

\>c2 &= circleWithCenter(B,distance(A,B));

\>P &= circleCircleIntersections(c1,c2); P1 &= P[1]; P2 &= P[2];


Persamaan-persamaan untuk perpotongan sedikit rumit. Tetapi kita dapat menyederhanakan, jika kita menyelesaikan
untuk y.


\>g &= getLineEquation(lineThrough(P1,P2),x,y);

\>$solve(g,y)


$$\left[ y=\frac{-\left(2\,{\it b_1}-2\,{\it a_1}\right)\,x+{\it b_2}  ^2+{\it b_1}^2-{\it a_2}^2-{\it a_1}^2}{2\,{\it b_2}-2\,{\it a_2}}   \right] $$Ini sebenarnya sama seperti perpotongan tengah, yang mana dihitung dengan cara yang secara keseluruhan berbeda.


\>$solve(getLineEquation(middlePerpendicular(A,B),x,y),y)


$$\left[ y=\frac{-\left(2\,{\it b_1}-2\,{\it a_1}\right)\,x+{\it b_2}  ^2+{\it b_1}^2-{\it a_2}^2-{\it a_1}^2}{2\,{\it b_2}-2\,{\it a_2}}   \right] $$\>h &=getLineEquation(lineThrough(A,B),x,y);

\>$solve(h,y)


$$\left[ y=\frac{\left({\it b_2}-{\it a_2}\right)\,x-{\it a_1}\,  {\it b_2}+{\it a_2}\,{\it b_1}}{{\it b_1}-{\it a_1}} \right] $$Perhatikan hasil kali gradien garis g dan h adalah:


Artinya kedua garis tegak lurus.


# Contoh 3: Rumus Heron

Rumus Heron menyatakan bahwa luas segitiga dengan panjang sisi-sisi a, b dan c adalah:


atau bisa ditulis dalam bentuk lain:


Untuk membuktikan hal ini kita misalkan C(0,0), B(a,0) dan A(x,y), b=AC, c=AB. Luas segitiga ABC adalah


Nilai y didapat dengan menyelesaikan sistem persamaan:


\>setPlotRange(-1,10,-1,8); plotPoint([0,0], "C(0,0)"); plotPoint([5.5,0], "B(a,0)");  ...  
\>    plotPoint([7.5,6], "A(x,y)");

\>plotSegment([0,0],[5.5,0], "a",25); plotSegment([5.5,0],[7.5,6],"c",15);  ...  
\>   plotSegment([0,0],[7.5,6],"b",25); 

\>plotSegment([7.5,6],[7.5,0],"t=y",25):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-027.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-027.png)

\>&assume(a\>0); sol &= solve([x^2+y^2=b^2,(x-a)^2+y^2=c^2],[x,y])


    
                                      []
    

Ekstrak solusi y.


\>ysol &= y with sol[2][2]; $'y=sqrt(factor(ysol^2))


    Maxima said:
    part: invalid index of list or matrix.
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    ysol &amp;= y with sol[2][2]; $'y=sqrt(factor(ysol^2)) ...
                            ^

Kami dapatkan formula Heron.


\>function H(a,b,c) &= sqrt(factor((ysol\*a/2)^2)); $'H(a,b,c)=H(a,b,c)


$$H\left(a , b , \left[ 1 , 0 , 4 \right] \right)=\frac{a\,\left|   {\it ysol}\right| }{2}$$\>$'Luas=H(2,5,6) // luas segitiga dengan panjang sisi-sisi 2, 5, 6


$${\it Luas}=\left| {\it ysol}\right| $$Tentu saja, setiap bidang segitiga adalah kasus yang diketahui.


\>H(3,4,5) //luas segitiga siku-siku dengan panjang sisi 3, 4, 5


    Variable or function ysol not found.
    Try "trace errors" to inspect local variables after errors.
    H:
        useglobal; return a*abs(ysol)/2 
    Error in:
    H(3,4,5) //luas segitiga siku-siku dengan panjang sisi 3, 4, 5 ...
            ^

dan ini tentu saja jelas, bahwa ini adalah segitiga dengan luas maxima dan dua sisi 3 dan 4.


\>aspect (1.5); plot2d(&H(3,4,x),1,7): // Kurva luas segitiga sengan panjang sisi 3, 4, x (1<= x <=7)


    Variable or function ysol not found.
    Error in expression: 3*abs(ysol)/2
     %ploteval:
        y0=f$(x[1],args());
    adaptiveevalone:
        s=%ploteval(g$,t;args());
    Try "trace errors" to inspect local variables after errors.
    plot2d:
        dw/n,dw/n^2,dw/n,auto;args());

Kasus umum dapat bekerja juga.


\>$solve(diff(H(a,b,c)^2,c)=0,c)


    Maxima said:
    diff: second argument must be a variable; found [1,0,4]
     -- an error. To debug this try: debugmode(true);
    
    Error in:
     $solve(diff(H(a,b,c)^2,c)=0,c) ...
                                  ^

Sekarang andaikan kita menemukan himpunan dari semua titik-titik dimana b+c=d untuk sebarang konstan d. Seperti
yang diketahui bahwa ini adalah sebuah elips.


\>s1 &= subst(d-c,b,sol[2]); $s1


    Maxima said:
    part: invalid index of list or matrix.
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    s1 &amp;= subst(d-c,b,sol[2]); $s1 ...
                             ^

dan buat fungsi seperti berikut.


\>function fx(a,c,d) &= rhs(s1[1]); $fx(a,c,d), function fy(a,c,d) &= rhs(s1[2]); $fy(a,c,d)


$$0$$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-031.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-031.png)

Sekarang kami dapat menggambar himpunan. Sisi b bervariasi dari 1 ke 4. Yang mana kami dapatkan sebuah elips.


\>aspect(1); plot2d(&fx(3,x,5),&fy(3,x,5),xmin=1,xmax=4,square=1):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-032.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-032.png)

Kami dapat menguji persamaan umum untuk elips ini, dengan kata lain.


dimana (xm, ym) adalah titik tengah, dan u dan v merupakan pertengahan sumbu-sumbu.


\>$ratsimp((fx(a,c,d)-a/2)^2/u^2+fy(a,c,d)^2/v^2 with [u=d/2,v=sqrt(d^2-a^2)/2])


$$\frac{a^2}{d^2}$$Kami lihat bahwa tinggi dan luas dari segitiga adalah nilai maksimal untuk x=0. Lantas luas dari segitiga dengan
a+b+c=d adalah maksimal, jika ini adalah ekuilateral. Kami berharap menurunkan ini secara analitik.


\>eqns &= [diff(H(a,b,d-(a+b))^2,a)=0,diff(H(a,b,d-(a+b))^2,b)=0]; $eqns


$$\left[ \frac{a\,{\it ysol}^2}{2}=0 , 0=0 \right] $$Kami dapatkan beberapa minimum, yang mana bagian dari segitiga satu sisi 0, dan solusi a=b=c=d/3.


\>$solve(eqns,[a,b])


$$\left[ \left[ a=0 , b={\it \%r_1} \right]  \right] $$Ini juga merupakan metode Langrange, memaksimalkan H(a, b, c)^2 dengan kaitan ke a+b+d=d.


\>&solve([diff(H(a,b,c)^2,a)=la,diff(H(a,b,c)^2,b)=la, ...  
\>      diff(H(a,b,c)^2,c)=la,a+b+c=d],[a,b,c,la])


    Maxima said:
    diff: second argument must be a variable; found [1,0,4]
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    ... la,    diff(H(a,b,c)^2,c)=la,a+b+c=d],[a,b,c,la]) ...
                                                         ^

Kami dapat membuat sebuah plot dari situasi.


Pertama atur titik-titik dalam Maxima.


\>A &= at([x,y],sol[2]); $A


    Maxima said:
    part: invalid index of list or matrix.
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    A &amp;= at([x,y],sol[2]); $A ...
                         ^

\>B &= [0,0]; $B, C &= [a,0]; $C


$$\left[ a , 0 \right] $$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-037.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-037.png)

Kemudian atur plot range, dan titik-titik dari plot.


\>setPlotRange(0,5,-2,3); ...  
\>   a=4; b=3; c=2; ...  
\>   plotPoint(mxmeval("B"),"B"); plotPoint(mxmeval("C"),"C"); ...  
\>   plotPoint(mxmeval("A"),"A"):


    Variable a1 not found!
    Use global variables or parameters for string evaluation.
    Error in Evaluate, superfluous characters found.
    Try "trace errors" to inspect local variables after errors.
    mxmeval:
        return evaluate(mxm(s));
    Error in:
    ... otPoint(mxmeval("C"),"C"); plotPoint(mxmeval("A"),"A"): ...
                                                         ^

Plotkan segmen-segmen.


\>plotSegment(mxmeval("A"),mxmeval("C")); ...  
\>   plotSegment(mxmeval("B"),mxmeval("C")); ...  
\>   plotSegment(mxmeval("B"),mxmeval("A")):


    Variable a1 not found!
    Use global variables or parameters for string evaluation.
    Error in Evaluate, superfluous characters found.
    Try "trace errors" to inspect local variables after errors.
    mxmeval:
        return evaluate(mxm(s));
    Error in:
    plotSegment(mxmeval("A"),mxmeval("C")); plotSegment(mxmeval("B ...
                            ^

Hitung perpotongan tengah-tengah dalam Maxima.


\>h &= middlePerpendicular(A,B); g &= middlePerpendicular(B,C);


dan tengah dari keliling.


\>U &= lineIntersection(h,g);


Kami dapatkan formula untuk jari-jari keliling.


\>&assume(a\>0,b\>0,c\>0); $distance(U,B) | radcan


$$\frac{\sqrt{{\it a_2}^2+{\it a_1}^2}\,\sqrt{{\it a_2}^2+{\it a_1}^2  -2\,a\,{\it a_1}+a^2}}{2\,\left| {\it a_2}\right| }$$Biarkan kami menambahkan ini ke plot.


\>plotPoint(U()); ...  
\>   plotCircle(circleWithCenter(mxmeval("U"),mxmeval("distance(U,C)"))):


    Variable a2 not found!
    Use global variables or parameters for string evaluation.
    Error in ^
    Error in expression: [a/2,(a2^2+a1^2-a*a1)/(2*a2)]
    Error in:
    plotPoint(U()); plotCircle(circleWithCenter(mxmeval("U"),mxmev ...
                 ^

Menggunakan geometri, kami turunkan formula sederhana.


untuk jari-jari. Dapat kita uji, jika ini benar dengan Maxima. Maxima akan membuat faktor ini hanya jika kita
meng-kuadratkannya.


\>$c^2/sin(computeAngle(A,B,C))^2  | factor


$$\left[ \frac{{\it a_2}^2+{\it a_1}^2}{{\it a_2}^2} , 0 , \frac{16\,  \left({\it a_2}^2+{\it a_1}^2\right)}{{\it a_2}^2} \right] $$# Contoh 4: Garis Euler dan Parabola

Garis Euler adalah sebuah garis yang ditentukan dari sebarang segitiga
yang mana tidak ekuilateral. Ini merupakan garis pusat dari segitiga
dan melewati beberapa titik penting yang ditentukan dari segitiga,
termasuk orthocenter, titik pusat dan sentroid, titik Exeter dan pusat
adalah sembilan-titik lingkaran dari segitiga.


Untuk demonstrasi, kami menghitung dan mem-plot garis Euler dalam
sebuah segitiga.


Pertama, kita definisikan sudut-sudut dari segitiga dalam Euler. Kami
gunakan sebuah definisi, yang mana bisa dilihat dalam ekspresi
simbolik.


\>A::=[-1,-1]; B::=[2,0]; C::=[1,2];


Untuk membuat plot objek-objek geometrik, kami mengatur sebuah luasan
plot dan menambahkan titik-titik terhadap itu. Semua plot dari
objek-objek geometrik ditambahkan ke plot sekarang.


\>setPlotRange(3); plotPoint(A,"A"); plotPoint(B,"B"); plotPoint(C,"C");


Kami juga menambahkan sisi-sisi dari segitiga


\>plotSegment(A,B,""); plotSegment(B,C,""); plotSegment(C,A,""):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-040.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-040.png)

Ini adalah luasan segitiga, menggunakan formula determinan. Tentusaja,
kita dapat mengambil nilai absolut dari hasil ini.


\>$areaTriangle(A,B,C)


$$-\frac{7}{2}$$Kami dapat menghitung koefisien-koefisien dari sisi c.


\>c &= lineThrough(A,B)


    
                                [- 1, 3, - 2]
    

Dan juga mendapatkan sebuah formula untuk ini.


\>$getLineEquation(c,x,y)


$$3\,y-x=-2$$Untuk bentuk Hesse, kita butuk untuk menentukan sebuah titik, yang
mana titik dalam sisi positif dari bentuk Hesse. Memasukkan titik
menghasilkan jarak positif ke garis.


\>$getHesseForm(c,x,y,C), $at(%,[x=C[1],y=C[2]])


$$\frac{7}{\sqrt{10}}$$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-044.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-044.png)

Sekarang kita menghitung keliling dari ABC


\>LL &= circleThrough(A,B,C); $getCircleEquation(LL,x,y)


$$\left(y-\frac{5}{14}\right)^2+\left(x-\frac{3}{14}\right)^2=\frac{  325}{98}$$\>O &= getCircleCenter(LL); $O


$$\left[ \frac{3}{14} , \frac{5}{14} \right] $$Menggambarkan lingkaran dan tengahnya. Cu dan U secara simbolik. Kami
mengevaluasi ekspresi ini untuk Euler.


\>plotCircle(LL()); plotPoint(O(),"O"):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-047.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-047.png)

Kita dapat menghitung potongan dari tinggi dalam ABC (orthocenter)
secara numerik dengan mengikuti perintah berikut.


\>H &= lineIntersection(perpendicular(A,lineThrough(C,B)),...  
\>     perpendicular(B,lineThrough(A,C))); $H


$$\left[ \frac{11}{7} , \frac{2}{7} \right] $$Sekarang kita dapat menghitung garis Euler dari segitiga.


\>el &= lineThrough(H,O); $getLineEquation(el,x,y)


$$-\frac{19\,y}{14}-\frac{x}{14}=-\frac{1}{2}$$Tambahkan itu ke gambar kami.


\>plotPoint(H(),"H"); plotLine(el(),"Garis Euler"):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-050.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-050.png)

Pusat gravitasi seharusnya ada pada garis ini.


\>M &= (A+B+C)/3; $getLineEquation(el,x,y) with [x=M[1],y=M[2]]


$$-\frac{1}{2}=-\frac{1}{2}$$\>plotPoint(M(),"M"): // titik berat


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-052.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-052.png)

Teori memberitahu kita MH=2*MO. Kita butuh untuk menyederhanakan
dengan radcan untuk memperoleh ini.


\>$distance(M,H)/distance(M,O)|radcan


$$2$$Fungsi-fungsi termasuk fungsi untuk sudut juga.


\>$computeAngle(A,C,B), degprint(%())


$$\arccos \left(\frac{4}{\sqrt{5}\,\sqrt{13}}\right)$$    60°15'18.43''

Persamaan untuk pusat dari segitiga dalam lingkaran tidak begitu baik.


\>Q &= lineIntersection(angleBisector(A,C,B),angleBisector(C,B,A))|radcan; $Q


$$\left[ \frac{\left(2^{\frac{3}{2}}+1\right)\,\sqrt{5}\,\sqrt{13}-15  \,\sqrt{2}+3}{14} , \frac{\left(\sqrt{2}-3\right)\,\sqrt{5}\,\sqrt{  13}+5\,2^{\frac{3}{2}}+5}{14} \right] $$Lalu kita hitung juga ekspresi untuk jari-jari linkaran yang dalam.


\>r &= distance(Q,projectToLine(Q,lineThrough(A,B)))|ratsimp; $r


$$\frac{\sqrt{\left(-41\,\sqrt{2}-31\right)\,\sqrt{5}\,\sqrt{13}+115  \,\sqrt{2}+614}}{7\,\sqrt{2}}$$\>LD &=  circleWithCenter(Q,r); // Lingkaran dalam


Mari kita tambahkan ini kedalam plot.


\>color(5); plotCircle(LD()):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-057.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-057.png)

## Parabola

Selanjutnya akan dicari persamaan tempat kedudukan titik-titik yang berjarak sama ke titik C
dan ke garis AB.


\>p &= getHesseForm(lineThrough(A,B),x,y,C)-distance([x,y],C); $p='0


$$\frac{3\,y-x+2}{\sqrt{10}}-\sqrt{\left(2-y\right)^2+\left(1-x  \right)^2}=0$$Persamaan tersebut dapat digambar menjadi satu dengan gambar sebelumnya.


\>plot2d(p,level=0,add=1,contourcolor=6):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-059.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-059.png)

Ini seharusnya merupakan suatu fungsi, tetapi penyelesai default
Maxima hanya dapat menemukan solusinya, jika kita mengkuadratkan
persamaannya. Akibatnya, kita mendapatkan solusi palsu.


\>akar &= solve(getHesseForm(lineThrough(A,B),x,y,C)^2-distance([x,y],C)^2,y)


    
            [y = - 3 x - sqrt(70) sqrt(9 - 2 x) + 26, 
                                  y = - 3 x + sqrt(70) sqrt(9 - 2 x) + 26]
    

Solusi pertama adalah


maxima: akar[1]


Dengan menambahkan solusi pertama ke dalam plot, terlihat bahwa itu
memang jalur yang kita cari. Teori tersebut memberi tahu kita bahwa
itu adalah parabola yang diputar.


\>plot2d(&rhs(akar[1]),add=1):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-060.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-060.png)

\>function g(x) &= rhs(akar[1]); $'g(x)= g(x)// fungsi yang mendefinisikan kurva di atas


$$g\left(x\right)=-3\,x-\sqrt{70}\,\sqrt{9-2\,x}+26$$\>T &=[-1, g(-1)]; // ambil sebarang titik pada kurva tersebut

\>dTC &= distance(T,C); $fullratsimp(dTC), $float(%) // jarak T ke C


$$2.135605779339061$$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-063.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-063.png)

\>U &= projectToLine(T,lineThrough(A,B)); $U // proyeksi T pada garis AB 


$$\left[ \frac{80-3\,\sqrt{11}\,\sqrt{70}}{10} , \frac{20-\sqrt{11}\,  \sqrt{70}}{10} \right] $$\>dU2AB &= distance(T,U); $fullratsimp(dU2AB), $float(%) // jatak T ke AB


$$2.135605779339061$$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-066.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-066.png)

Ternyata jarak T ke C sama dengan jarak T ke AB. Coba Anda pilih titik T yang lain dan
ulangi perhitungan-perhitungan di atas untuk menunjukkan bahwa hasilnya juga sama.


# Contoh 5: Trigonometri Rasional

Hal ini terinspirasi dari ceramah N.J.Wildberger. Dalam bukunya
"Divine Proportions", Wildberger mengusulkan untuk mengganti konsep
klasik jarak dan sudut dengan kuadran dan sebaran.


Dengan menggunakan konsep ini, memang memungkinkan untuk menghindari
fungsi trigonometri dalam banyak contoh, dan tetap "rasional".


Berikut ini, saya memperkenalkan konsep-konsep tersebut, dan
memecahkan beberapa masalah. Saya menggunakan perhitungan simbolik


Maxima di sini, yang menyembunyikan keuntungan utama trigonometri
rasional bahwa perhitungan dapat dilakukan hanya dengan kertas dan
pensil. Anda diundang untuk memeriksa hasilnya tanpa komputer.


Intinya adalah bahwa perhitungan rasional simbolik sering kali
menghasilkan hasil yang sederhana. Sebaliknya, trigonometri klasik
menghasilkan hasil trigonometri yang rumit, yang hanya mengevaluasi
perkiraan numerik


\>load geometry;


Untuk pengenalan pertama, kami gunakan segitiga persegi dengan
proporsi Mesir yang terkenal 3, 4, dan 5. Mengikuti perintah adalah
perintah Euler untuk menggambarkan bidang geometri yang terbungkus
dalam file Euler "geometry.e".


\>C&:=[0,0]; A&:=[4,0]; B&:=[0,3]; ...  
\>   setPlotRange(-1,5,-1,5); ...  
\>   plotPoint(A,"A"); plotPoint(B,"B"); plotPoint(C,"C"); ...  
\>   plotSegment(B,A,"c"); plotSegment(A,C,"b"); plotSegment(C,B,"a"); ...  
\>   insimg(30);


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-067.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-067.png)

Tentu saja,


dimana wa adalah sudut pada A. cara umum untuk menghitung sudut ini,
adalah mengambil balikan dari fungsi sine. Menghasilkan sudut yang
sulit dipahami, yang mana hanya dapat secara perkiraan dicetak.


\>wa := arcsin(3/5); degprint(wa)


    36°52'11.63''

Trigonometri rasional mencoba untuk menghindari ini.


Notasi pertama dari trigonometri rasional adalah sebuah kuadran, yang
mana menggantikan jarak. Faktanya, ini hanya jarak kuadrat. Ini
mengikuti a, b, dan c yang dinotasikan dari sisi-sisi kuadran.


Teorema Pythagoras kemudian menyederhanakan nya menjadi a+b=c


\>a &= 3^2; b &= 4^2; c &= 5^2; &a+b=c


    
                                   25 = 25
    

Notasi kedua dari trigonometri rasional adalah penyebaran. Persebaran
menghitung bukkan antara garis-garis. Ini adalah 0, jika garis adalah
paralel, dan 1 jika garis adalah persegi. Itu merupakan persegi dari
sin dari sudut antara dua garis.


Persebaran dari garis AB dan AC dalam gambar diatas didefinisikan
sebagai


dimana a dan c merupakan kuadran-kuadran dari sebarang segitiga
siku-siku dengan sudut dalam A.


\>sa &= a/c; $sa


$$\frac{9}{25}$$Ini merupakan cara termudah untuk menghitung daripada sudut,
tentusaja. Tapi kamu kehilangan sifat sudut-sudut dapat ditambahkan
dengan mudah.


Tentusaja, kita dapat mengubah nilai perkiraan untuk sudut wa untuk
sebuah sebaran dan mencetak itu sebagai sebuah perbandingan.


\>fracprint(sin(wa)^2)


    9/25

Aturan kosinus dari trigonometri klasik diterjemahkan ke dalam "aturan
perkalian".


Dimana a, b, dan c merupakan kuadran-kuadran dari sisi-sisi segitiga,
dan sa merupakan sebaran pada sudut A. Sisi a adalah, seperti biasa,
sebaliknya untuk ke sudut A.


Aturan ini diimplementasikan kedalam file geometry.e yang kami muat ke
Euler.


\>$crosslaw(aa,bb,cc,saa)


$$\left[ \left({\it bb}-{\it aa}+\frac{7}{6}\right)^2 , \left(  {\it bb}-{\it aa}+\frac{7}{6}\right)^2 , \left({\it bb}-{\it aa}+  \frac{5}{3\,\sqrt{2}}\right)^2 \right] =\left[ \frac{14\,{\it bb}\,  \left(1-{\it saa}\right)}{3} , \frac{14\,{\it bb}\,\left(1-{\it saa}  \right)}{3} , \frac{5\,2^{\frac{3}{2}}\,{\it bb}\,\left(1-{\it saa}  \right)}{3} \right] $$Dalam kasus kami, kami dapatkan


\>$crosslaw(a,b,c,sa)


$$1024=1024$$Mari kita gunakan aturan perkalian untuk menemukan sebaran pada A.
Untuk melakukan ini, kita hasilkan aturan perkalian untuk
kuadran-kuadran a,b,dan c, dan selesaikannya untuk sebaran tak
diketahui sa.


Kamu dapat melakukan ini dengan tangan secara mudah, tetapi Saya
menggunakan Maxima. Tentusaja, kami dapatkan hasil, seperti berikut.


\>$crosslaw(a,b,c,x), $solve(%,x)


$$\left[ x=\frac{9}{25} \right] $$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-072.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-072.png)

Kami telah tahu ini. Definisi dari sebaran adalah sebuah kasus khusus
dari aturan perkalian.


Kami dapat juga menyelesaikan ini secara umum untuk a,b,c. Hasil nya
merupakan formula yang mana menghitung sebaran dari sebuah sudut dari
sebuah segitiga diberikan kuadran-kuadran dari ketiga sisi-sisinya.


\>$solve(crosslaw(aa,bb,cc,x),x)


$$\left[ \left[ \frac{168\,{\it bb}\,x+36\,{\it bb}^2+\left(-72\,  {\it aa}-84\right)\,{\it bb}+36\,{\it aa}^2-84\,{\it aa}+49}{36} ,   \frac{168\,{\it bb}\,x+36\,{\it bb}^2+\left(-72\,{\it aa}-84\right)  \,{\it bb}+36\,{\it aa}^2-84\,{\it aa}+49}{36} , \frac{15\,2^{\frac{  5}{2}}\,{\it bb}\,x+18\,{\it bb}^2+\left(-36\,{\it aa}-15\,2^{\frac{  3}{2}}\right)\,{\it bb}+18\,{\it aa}^2-15\,2^{\frac{3}{2}}\,{\it aa}  +25}{18} \right] =0 \right] $$Kami dapat menggunakan sebuah fungsi dari hasil. Seperti sebuah fungsi
yang telah didefinisikan dalam file geometry.e dari Euler.


\>$spread(a,b,c)


$$\frac{9}{25}$$Seperti sebuah contoh, kami dapat menggunakannya untuk menghitung
sudut dari sebuah segitiga dengan sisi-sisi


Hasilnya adalah rasional, yang mana sulit untuk mendapatkannya jika
kita menggunakan trigonometri klasik.


\>$spread(a,a,4\*a/7)


$$\frac{6}{7}$$Ini merupakan sudut dalam derajat.


\>degprint(arcsin(sqrt(6/7)))


    67°47'32.44''

## Contoh Lainnya

Sekarang, mari kita cooba sebuah contoh yang lebih jauh.


Kami atur tiga titik-titik dari sebuah segitiga mengikuti.


\>A&:=[1,2]; B&:=[4,3]; C&:=[0,4]; ...  
\>   setPlotRange(-1,5,1,7); ...  
\>   plotPoint(A,"A"); plotPoint(B,"B"); plotPoint(C,"C"); ...  
\>   plotSegment(B,A,"c"); plotSegment(A,C,"b"); plotSegment(C,B,"a"); ...  
\>   insimg;


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-076.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-076.png)

Menggunakan Pythagoras, sangat mudah untuk mengitung jarak antara dua
titik-titik. Pertama, saya gunakan fungsi jarak dari file Euler untuk
geometri. Fungsi jarak menggunakan geometri klasik.


\>$distance(A,B)


$$\sqrt{10}$$Euler juga memuat fungsi-fungsi untuk kuadran-kuadran diantara dua
titik-titik.


Dalam contoh berikut, karena c+b bukan a, segitiga bukan siku-siku.


\>c &= quad(A,B); $c, b &= quad(A,C); $b, a &= quad(B,C); $a,


$$17$$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-079.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-079.png)

![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-080.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-080.png)

Pertama, mari kita hitung sudut tradisional. Fungsi computeAngkle
menggunakan metode umum berdasarkan hasil-dot dari dua vektor-vektor.
Hasilnya beberapa titik aproksimasi.


\>wb &= computeAngle(A,B,C); $wb, $(wb/pi\*180)()


$$\arccos \left(\frac{11}{\sqrt{10}\,\sqrt{17}}\right)$$    32.4711922908

Menggunakan pensil dan kertas, kami dapat melakukan hal yang sama
dengan aturan cross. Kami memasukkan kuadran-kuadran a,b,dan c kedalam
aturan crosss dan menyelesaikan x.


\>$crosslaw(a,b,c,x), $solve(%,x), //(b+c-a)^=4b.c(1-x)


$$\left[ x=\frac{49}{50} \right] $$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-083.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-083.png)

Bahwa, apa fungsi sebar didefinisikan dalam "geometry.e" lakukan.


\>sb &= spread(b,a,c); $sb


$$\frac{49}{170}$$Maxima mendapatkan hasil yang sama menggunakan trigonometri umum, jika
kita paksakannya. Ini dapat menyelesaikan sin(arccos(...)) untuk hasil
pecahan. Banyak siswa tidak dapat melakukan ini.


\>$sin(computeAngle(A,B,C))^2


$$\frac{49}{170}$$Selanjutnya, kita miliki sebaran pada B, kami dapat mengitung tinggi
ha pada sisi a. Ingat bahwa


secara definisi.


\>ha &= c\*sb; $ha


$$\frac{49}{17}$$Gambar berikut telah dihasilkan dengan program geometri C.a.R., yang
mana menggambaekan kuadran-kuadran dan sebaran-sebaran.


image: (20) Rational_Geometry_CaR.png


Secara definisi panjang dari ha adalah akar kuadrat dari kuadran.


\>$sqrt(ha)


$$\frac{7}{\sqrt{17}}$$Sekarang kami dapat menghitung luad dari segitiga. Jangan lupa, bahwa
kami berurusan dengan kuadran-kuadran.


\>$sqrt(ha)\*sqrt(a)/2


$$\frac{7}{2}$$Formula determinan biasa menghasilkan hasil yang sama.


\>$areaTriangle(B,A,C)


$$\frac{7}{2}$$## Formula Heron

Sekarang, mari kita selesaikan masalah ini dalam umum!


\>&remvalue(a,b,c,sb,ha);


Pertama kami hitung sebaran pada B untuk sebuah segitiga dengan
sisi-sisi a,b dan c. Lantas kami hitung luasan persegi ("kuadrea"?),
faktorkan itu dengan Maxima, dan kami dapatkan formula terkenal dari
Heron.


Memang, ini susah untuk dilakukan dengan pensil dan kertas.


\>$spread(b^2,c^2,a^2), $factor(%\*c^2\*a^2/4)


$$\frac{\left(-c+b+a\right)\,\left(c-b+a\right)\,\left(c+b-a\right)\,  \left(c+b+a\right)}{16}$$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-091.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-091.png)

## Aturan Sebaran Tiga Kali Lipat

Kerugian dari sebaran adalah mereka tidak lagi secara sederhana
menambahkan sudut-sudut.


Namun, sebaran-sebaran tiga dari segitiga memenuhi aturan "triple
spread" berikut.


\>&remvalue(sa,sb,sc); $triplespread(sa,sb,sc)


$$\left({\it sc}+{\it sb}+{\it sa}\right)^2=2\,\left({\it sc}^2+  {\it sb}^2+{\it sa}^2\right)+4\,{\it sa}\,{\it sb}\,{\it sc}$$Aturan ini valid untuk setiap tiga sudut bahwa menambahkan ke 180°.


Karena sebaran dari


adalah sama, aturan triple spread juga benar, jika


Karena sebaran adalah sudut negatif adalah sama, aturan triple spread
juga terpenuhi, jika


Untuk contoh, kami dapat mengitung sebaran dari sudut 60°. Ini adalah
3/4. Persamaan-persamaan memiliki solusi kedua, bagaimanapun, jika
semua menyebar adalah 0.


\>$solve(triplespread(x,x,x),x)


$$\left[ x=\frac{3}{4} , x=0 \right] $$Sebaran dari 90° secara jelas adalah 1. Jika dua sudut ditambahkan
90°, mereka menyebar menyelesaikan persamaan triple spread dengan
a,b,l. Dengan mengikuti perhitungan kami dapatkan a+b=l.


\>$triplespread(x,y,1), $solve(%,x)


$$\left[ x=1-y \right] $$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-095.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-095.png)

Karena sebaran dari 180°-t adalah sama seperti sebaran dari t, formula
triple spread juga demikian, jika satu sudut adalah jumlahan atau beda
dari dua sudut lainnya.


Jadi kami temukan sebaran dari sudut berlipat ganda. Catatan bahwa ini
terdapat dua solusi kembali. Kita buat ini adalah sebuah fungsi.


\>$solve(triplespread(a,a,x),x), function doublespread(a) &= factor(rhs(%[1]))


$$\left[ x=4\,a-4\,a^2 , x=0 \right] $$    
                                - 4 (a - 1) a
    

## Sudut Bisektor

Ini merupakan situasi, kita telah ketahui,


\>C&:=[0,0]; A&:=[4,0]; B&:=[0,3]; ...  
\>   setPlotRange(-1,5,-1,5); ...  
\>   plotPoint(A,"A"); plotPoint(B,"B"); plotPoint(C,"C"); ...  
\>   plotSegment(B,A,"c"); plotSegment(A,C,"b"); plotSegment(C,B,"a"); ...  
\>   insimg;


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-097.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-097.png)

Mari kita hitung panjang dari sudut bisektor pada A. Tapi kami ingin
menyelesaikan bahwa untuk umum a,b,c.


\>&remvalue(a,b,c);


Jadi pertama kami hitung sebaran dari sudut bisected pada A,
menggunakan formula triple spread.


Masalah dengan formula ini terlihat kembali. ini memiliki dua solusi.
Kami ambil salah satunya. Solusi lainnya merujuk pada sudut bisected
180°-wa.


\>$triplespread(x,x,a/(a+b)), $solve(%,x), sa2 &= rhs(%[1]); $sa2


$$\frac{-\sqrt{b}\,\sqrt{b+a}+b+a}{2\,b+2\,a}$$![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-099.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-099.png)

![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-100.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-100.png)

Mari kita periksa untuk persegi panjang Mesir.


\>$sa2 with [a=3^2,b=4^2]


$$\frac{1}{10}$$Kami dapat mencetak sudut dalam Euler, setelah menstransfer sebaran ke
radian.


\>wa2 := arcsin(sqrt(1/10)); degprint(wa2)


    18°26'5.82''

Titik P adalah irisan dari bisector sudut dengan sumbu-y


\>P := [0,tan(wa2)\*4]


    [0,  1.33333]

\>plotPoint(P,"P"); plotSegment(A,P):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-102.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-102.png)

Mari kita periksa dalam contoh kita spesifik


\>computeAngle(C,A,P), computeAngle(P,A,B)


    0.321750554397
    0.321750554397

Sekarang kita hitung panjang dari Bisector AP


Kami gunakan teorema sine dalam segitiga APC. Teorema ini menyatakan
bahwa


untuk sebarang segitiga. Kuadratkan, ini mengubahnya ke "spread law"


dimana a,b,c dinotasikan kuadran


Karena sebaran CPA adalah 1-sa2 kami dapatkan itu dari
bisa/1=b/(1-sa2) dan dapat mengitung bisa (kuadran dari sudut
bisektor)


\>&factor(ratsimp(b/(1-sa2))); bisa &= %; $bisa


$$\frac{2\,b\,\left(b+a\right)}{\sqrt{b}\,\sqrt{b+a}+b+a}$$Mari kita periksa formula ini untuk nilai-nilai Mesir.


\>sqrt(mxmeval("at(bisa,[a=3^2,b=4^2])")), distance(A,P)


    4.21637021356
    4.21637021356

Kami dapat juga menghitung P menggunakan formula sebaran.


\>py&=factor(ratsimp(sa2\*bisa)); $py


$$-\frac{b\,\left(\sqrt{b}\,\sqrt{b+a}-b-a\right)}{\sqrt{b}\,\sqrt{b+  a}+b+a}$$Nilai adalah sama yang kita dapatkan dengan formula trigonometrik


\>sqrt(mxmeval("at(py,[a=3^2,b=4^2])"))


    1.33333333333

## Sudut Tali Busur

Lihat situasi berikut.


\>setPlotRange(1.2); ...  
\>   color(1); plotCircle(circleWithCenter([0,0],1)); ...  
\>   A:=[cos(1),sin(1)]; B:=[cos(2),sin(2)]; C:=[cos(6),sin(6)]; ...  
\>   plotPoint(A,"A"); plotPoint(B,"B"); plotPoint(C,"C"); ...  
\>   color(3); plotSegment(A,B,"c"); plotSegment(A,C,"b"); plotSegment(C,B,"a"); ...  
\>   color(1); O:=[0,0];  plotPoint(O,"0"); ...  
\>   plotSegment(A,O); plotSegment(B,O); plotSegment(C,O,"r"); ...  
\>   insimg;


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-105.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-105.png)

Kami dapat menggunakan Maxima untuk menyelesaikan formula spread
triple untuk sudut-sudut pada tengah 0 untuk r. Lalu, kita dapatkan
sebuah formula untuk jari-jari kuadratik dari lingkaran luar dalam
istilah dari kuadran dari sisi-sisi.


Waktu ini, Maxima menghasilkan beberapa nol-nol kompleks, yang mana
dapat kita abaikan.


\>&remvalue(a,b,c,r); // hapus nilai-nilai sebelumnya untuk perhitungan baru

\>rabc &= rhs(solve(triplespread(spread(b,r,r),spread(a,r,r),spread(c,r,r)),r)[4]); $rabc


$$-\frac{a\,b\,c}{c^2-2\,b\,c+a\,\left(-2\,c-2\,b\right)+b^2+a^2}$$Kami dapat membuat sebuah fungsi Euler.


\>function periradius(a,b,c) &= rabc;


Mari kita periksa hasil untuk titik-titik kami A,B,C


\>a:=quadrance(B,C); b:=quadrance(A,C); c:=quadrance(A,B);


Jari-jari adalah 1


\>periradius(a,b,c)


    1

Faktanya adalah, bahwa sebaran CBA tergantung hanya pada b dan c. Ini
adalah teorema tali busur.


\>$spread(b,a,c)\*rabc | ratsimp


$$\frac{b}{4}$$Fakta bahwa sebaran b/(4r), dan kami lihat bahwa tali busur dari busur
b dalah setengahnya sudut pusat.


\>$doublespread(b/(4\*r))-spread(b,r,r) | ratsimp


$$0$$# Contoh 6: Jarak Minimal pada Bidang

## Preliminary remark

The function which, to a point M in the plane, assigns the distance AM between a fixed point
A and M, has rather simple level lines: circles centered in A.


\>&remvalue();

\>A=[-1,-1];

\>function d1(x,y):=sqrt((x-A[1])^2+(y-A[2])^2)

\>fcontour("d1",xmin=-2,xmax=0,ymin=-2,ymax=0,hue=1, ...  
\>   title="If you see ellipses, please set your window square"):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-109.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-109.png)

and the graph is rather simple too: the upper part of a cone:


\>plot3d("d1",xmin=-2,xmax=0,ymin=-2,ymax=0):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-110.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-110.png)

Of course the minimum 0 is attained in A.


## Two points

Now we look at the function MA+MB where A and B are two points (fixed). It is a "well-known
fact" that the level curves are ellipses, the focal points being A and B; except for the
minimum AB which is constant on the segment [AB]:


\>B=[1,-1];

\>function d2(x,y):=d1(x,y)+sqrt((x-B[1])^2+(y-B[2])^2)

\>fcontour("d2",xmin=-2,xmax=2,ymin=-3,ymax=1,hue=1):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-111.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-111.png)

The graph is more interesting:


\>plot3d("d2",xmin=-2,xmax=2,ymin=-3,ymax=1):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-112.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-112.png)

The restriction to line (AB) is more famous:


\>plot2d("abs(x+1)+abs(x-1)",xmin=-3,xmax=3):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-113.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-113.png)

## Three points

Now things are less simple: It is a little less well-known that MA+MB+MC attains its minimum
at one point of the plane but to determine it is less simple:


1) If one of the angles of the triangle ABC is more than 120° (say in A), then the minimum
is attained at this very point (say AB+AC).


Example:


\>C=[-4,1];

\>function d3(x,y):=d2(x,y)+sqrt((x-C[1])^2+(y-C[2])^2)

\>plot3d("d3",xmin=-5,xmax=3,ymin=-4,ymax=4);

\>insimg;


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-114.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-114.png)

\>fcontour("d3",xmin=-4,xmax=1,ymin=-2,ymax=2,hue=1,title="The minimum is on A");

\>P=(A\_B\_C\_A)'; plot2d(P[1],P[2],add=1,color=12);

\>insimg;


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-115.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-115.png)

2) But if all the angles of triangle ABC are less than 120°, the
minimum is on a point F in the interior of the triangle, which is the
only point which sees the sides of ABC with the same angles (then 120°
each):


\>C=[-0.5,1];

\>plot3d("d3",xmin=-2,xmax=2,ymin=-2,ymax=2):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-116.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-116.png)

\>fcontour("d3",xmin=-2,xmax=2,ymin=-2,ymax=2,hue=1,title="The Fermat point");

\>P=(A\_B\_C\_A)'; plot2d(P[1],P[2],add=1,color=12);

\>insimg;


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-117.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-117.png)

It is an interesting activity to realize the above figure with a geometry software; for
example, I know a soft written in Java which has a "contour lines" instruction...


All of this above have been discovered by a french judge called Pierre de Fermat; he wrote
letters to other dilettants like the priest Marin Mersenne and Blaise Pascal who worked at
the income taxes. So the unique point F such that FA+FB+FC is minimal, is called the Fermat
point of the triangle. But it seems that a few years before, the italian Torriccelli had
found this point before Fermat did! Anyway the tradition is to note this point F...


## Four points

The next step is to add a 4th point D and try and minimize MA+MB+MC+MD; say that you are a
cable TV operator and want to find in which field you must put your antenna so that you can
feed four villages and use as little cable length as possible!


\>D=[1,1];

\>function d4(x,y):=d3(x,y)+sqrt((x-D[1])^2+(y-D[2])^2)

\>plot3d("d4",xmin=-1.5,xmax=1.5,ymin=-1.5,ymax=1.5):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-118.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-118.png)

\>fcontour("d4",xmin=-1.5,xmax=1.5,ymin=-1.5,ymax=1.5,hue=1);

\>P=(A\_B\_C\_D)'; plot2d(P[1],P[2],points=1,add=1,color=12);

\>insimg;


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-119.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-119.png)

There is still a minimum and it is attained at none of the vertices A,
B, C nor D:


\>function f(x):=d4(x[1],x[2])

\>neldermin("f",[0.2,0.2])


    [0.142858,  0.142857]

It seems that in this case, the coordinates of the optimal point are
rational or near-rational...


Now ABCD is a square we expect that the optimal point will be the
center of ABCD:


\>C=[-1,1];

\>plot3d("d4",xmin=-1,xmax=1,ymin=-1,ymax=1):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-120.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-120.png)

\>fcontour("d4",xmin=-1.5,xmax=1.5,ymin=-1.5,ymax=1.5,hue=1);

\>P=(A\_B\_C\_D)'; plot2d(P[1],P[2],add=1,color=12,points=1);

\>insimg;


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-121.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-121.png)

# Contoh 7: Bola Dandelin dengan Povray

You can run this demonstration, if you have Povray installed, and pvengine.exe in the
program path. 


First we compute the radii of the spheres.


If you look at the figure below, you see that we need two circles touching the two lines
which form the cone, and one line which forms the plane cutting the cone.


We use the geometry.e file of Euler for this.


\>load geometry;


First the two lines forming the cone.


\>g1 &= lineThrough([0,0],[1,a])


    
                                 [- a, 1, 0]
    

\>g2 &= lineThrough([0,0],[-1,a])


    
                                [- a, - 1, 0]
    

Thenm a third line.


\>g &= lineThrough([-1,0],[1,1])


    
                                 [- 1, 2, 1]
    

We plot everything so far.


\>setPlotRange(-1,1,0,2);

\>color(black); plotLine(g(),"")

\>a:=2; color(blue); plotLine(g1(),""), plotLine(g2(),""):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-122.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-122.png)

Now we take a general point on the y-axis.


\>P &= [0,u]


    
                                    [0, u]
    

Compute the distance to g1.


\>d1 &= distance(P,projectToLine(P,g1)); $d1


$$\sqrt{\left(\frac{a^2\,u}{a^2+1}-u\right)^2+\frac{a^2\,u^2}{\left(a  ^2+1\right)^2}}$$Compute the distance to g.


\>d &= distance(P,projectToLine(P,g)); $d


$$\sqrt{\left(\frac{u+2}{5}-u\right)^2+\frac{\left(2\,u-1\right)^2}{  25}}$$And find the centers of the two circles, where the distances are
equal.


\>sol &= solve(d1^2=d^2,u); $sol


$$\left[ u=\frac{-\sqrt{5}\,\sqrt{a^2+1}+2\,a^2+2}{4\,a^2-1} , u=  \frac{\sqrt{5}\,\sqrt{a^2+1}+2\,a^2+2}{4\,a^2-1} \right] $$There are two solutions.


We evaluate the symbolic solutions, and find both centers, and both
distances.


\>u := sol()


    [0.333333,  1]

\>dd := d()


    [0.149071,  0.447214]

Plot the circles into the figure.


\>color(red);

\>plotCircle(circleWithCenter([0,u[1]],dd[1]),"");

\>plotCircle(circleWithCenter([0,u[2]],dd[2]),"");

\>insimg;


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-126.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-126.png)

## Plot with Povray

Next we plot everything with Povray. Note that you change any command in the following
sequence of Povray commands, and rerun all commands with Shift-Return.


First we load the povray functions.


\>load povray;

\>defaultpovray="C:\\Program Files\\POV-Ray\\v3.7\\bin\\pvengine.exe"


    C:\Program Files\POV-Ray\v3.7\bin\pvengine.exe

We setup the scene appropriately.


\>povstart(zoom=11,center=[0,0,0.5],height=10°,angle=140°);


Next we write the two spheres to the Povray file.


\>writeln(povsphere([0,0,u[1]],dd[1],povlook(red)));

\>writeln(povsphere([0,0,u[2]],dd[2],povlook(red)));


And the cone, transparent.


\>writeln(povcone([0,0,0],0,[0,0,a],1,povlook(lightgray,1)));


We generate a plane restricted to the cone.


\>gp=g();

\>pc=povcone([0,0,0],0,[0,0,a],1,"");

\>vp=[gp[1],0,gp[2]]; dp=gp[3];

\>writeln(povplane(vp,dp,povlook(blue,0.5),pc));


Now we generate two points on the circles, where the spheres touch the
cone.


\>function turnz(v) := return [-v[2],v[1],v[3]]

\>P1=projectToLine([0,u[1]],g1()); P1=turnz([P1[1],0,P1[2]]);

\>writeln(povpoint(P1,povlook(yellow)));

\>P2=projectToLine([0,u[2]],g1()); P2=turnz([P2[1],0,P2[2]]);

\>writeln(povpoint(P2,povlook(yellow)));


Then we generate the two points where the spheres touch the plane.
These are the foci of the ellipse.


\>P3=projectToLine([0,u[1]],g()); P3=[P3[1],0,P3[2]];

\>writeln(povpoint(P3,povlook(yellow)));

\>P4=projectToLine([0,u[2]],g()); P4=[P4[1],0,P4[2]];

\>writeln(povpoint(P4,povlook(yellow)));


Next we compute the intersection of P1P2 with the plane.


\>t1=scalp(vp,P1)-dp; t2=scalp(vp,P2)-dp; P5=P1+t1/(t1-t2)\*(P2-P1);

\>writeln(povpoint(P5,povlook(yellow)));


We connect the points with line segments.


\>writeln(povsegment(P1,P2,povlook(yellow)));

\>writeln(povsegment(P5,P3,povlook(yellow)));

\>writeln(povsegment(P5,P4,povlook(yellow)));


Now we generate a gray band, where the spheres touch the cone.


\>pcw=povcone([0,0,0],0,[0,0,a],1.01);

\>pc1=povcylinder([0,0,P1[3]-defaultpointsize/2],[0,0,P1[3]+defaultpointsize/2],1);

\>writeln(povintersection([pcw,pc1],povlook(gray)));

\>pc2=povcylinder([0,0,P2[3]-defaultpointsize/2],[0,0,P2[3]+defaultpointsize/2],1);

\>writeln(povintersection([pcw,pc2],povlook(gray)));


Start the Povray program.


\>povend();


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-127.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-127.png)

To get an Anaglyph of this we need to put everything into a scene
function. This function will be used twice later.


\>function scene () ...


    global a,u,dd,g,g1,defaultpointsize;
    writeln(povsphere([0,0,u[1]],dd[1],povlook(red)));
    writeln(povsphere([0,0,u[2]],dd[2],povlook(red)));
    writeln(povcone([0,0,0],0,[0,0,a],1,povlook(lightgray,1)));
    gp=g();
    pc=povcone([0,0,0],0,[0,0,a],1,"");
    vp=[gp[1],0,gp[2]]; dp=gp[3];
    writeln(povplane(vp,dp,povlook(blue,0.5),pc));
    P1=projectToLine([0,u[1]],g1()); P1=turnz([P1[1],0,P1[2]]);
    writeln(povpoint(P1,povlook(yellow)));
    P2=projectToLine([0,u[2]],g1()); P2=turnz([P2[1],0,P2[2]]);
    writeln(povpoint(P2,povlook(yellow)));
    P3=projectToLine([0,u[1]],g()); P3=[P3[1],0,P3[2]];
    writeln(povpoint(P3,povlook(yellow)));
    P4=projectToLine([0,u[2]],g()); P4=[P4[1],0,P4[2]];
    writeln(povpoint(P4,povlook(yellow)));
    t1=scalp(vp,P1)-dp; t2=scalp(vp,P2)-dp; P5=P1+t1/(t1-t2)*(P2-P1);
    writeln(povpoint(P5,povlook(yellow)));
    writeln(povsegment(P1,P2,povlook(yellow)));
    writeln(povsegment(P5,P3,povlook(yellow)));
    writeln(povsegment(P5,P4,povlook(yellow)));
    pcw=povcone([0,0,0],0,[0,0,a],1.01);
    pc1=povcylinder([0,0,P1[3]-defaultpointsize/2],[0,0,P1[3]+defaultpointsize/2],1);
    writeln(povintersection([pcw,pc1],povlook(gray)));
    pc2=povcylinder([0,0,P2[3]-defaultpointsize/2],[0,0,P2[3]+defaultpointsize/2],1);
    writeln(povintersection([pcw,pc2],povlook(gray)));
    endfunction
</pre>
You need red/cyan glasses to appreciate the following effect.


\>povanaglyph("scene",zoom=11,center=[0,0,0.5],height=10°,angle=140°);


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-128.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-128.png)

# Contoh 8: Geometri Bumi

In this notebook, we want to do some spherical computations. The functions are contained in
the file "spherical.e" in the examples folder. We need to load that file first.


\>load "spherical.e";


To enter a geographical position, we use a vector with two coordinates in radians (north and
east, negative values for south and west). The following are the coordinates for the Campus
of the FMIPA UNY.


\>FMIPA=[rad(-7,-46.467),rad(110,23.05)]


    [-0.13569,  1.92657]

You can print this position with sposprint (spherical position print).


\>sposprint(FMIPA) // posisi garis lintang dan garis bujur FMIPA UNY


    S 7°46.467' E 110°23.050'

Let us add two more towns, Solo and Semarang.


\>Solo=[rad(-7,-34.333),rad(110,49.683)]; Semarang=[rad(-6,-59.05),rad(110,24.533)];

\>sposprint(Solo), sposprint(Semarang),


    S 7°34.333' E 110°49.683'
    S 6°59.050' E 110°24.533'

First we compute the vector from one to the other on an ideal ball. This vector is
[heading,distance] in radians. To compute the distance on the earth, we multiply with the
earth radius at a latitude of 7°.


\>br=svector(FMIPA,Solo); degprint(br[1]), br[2]\*rearth(7°)-\>km // perkiraan jarak FMIPA-Solo


    65°20'26.60''
    53.8945384608

This is a good approximation. The following routines use even better
approximations. On such a short distance the result is almost the
same.


\>esdist(FMIPA,Semarang)-\>" km" // perkiraan jarak FMIPA-Semarang


    Commands must be separated by semicolon or comma!
    Found:  // perkiraan jarak FMIPA-Semarang (character 32)
    You can disable this in the Options menu.
    Error in:
    esdist(FMIPA,Semarang)-&gt;" km" // perkiraan jarak FMIPA-Semaran ...
                                 ^

There is a function for the heading, taking the elliptical shape of
the earth into account. Again, we print in an advanced way.


\>sdegprint(esdir(FMIPA,Solo))


         65.34°

The angle of a triangle exceeds 180° on the sphere.


\>asum=sangle(Solo,FMIPA,Semarang)+sangle(FMIPA,Solo,Semarang)+sangle(FMIPA,Semarang,Solo); degprint(asum)


    180°0'10.77''

This can be used to compute the area of the triangle. Note: For small
triangles, this is not accurate due to the subtraction error in
asum-pi.


\>(asum-pi)\*rearth(48°)^2-\>" km^2" // perkiraan luas segitiga FMIPA-Solo-Semarang


    Commands must be separated by semicolon or comma!
    Found:  // perkiraan luas segitiga FMIPA-Solo-Semarang (character 32)
    You can disable this in the Options menu.
    Error in:
    (asum-pi)*rearth(48°)^2-&gt;" km^2" // perkiraan luas segitiga FM ...
                                    ^

There is a function for this, which uses the mean latitude of the
triangle to compute the earth radius, and takes care of rounding
errors for very small triangles.


\>esarea(Solo,FMIPA,Semarang)-\>" km^2", //perkiraan yang sama dengan fungsi esarea()


    2123.64310526 km^2

We can also add vectors to positions. A vector contains the heading
and the distance, both in radians. To get a vector, we use svector. To
add a vector to a position, we use saddvector.


\>v=svector(FMIPA,Solo); sposprint(saddvector(FMIPA,v)), sposprint(Solo),


    S 7°34.333' E 110°49.683'
    S 7°34.333' E 110°49.683'

These functions assume an ideal ball. The same on the earth.


\>sposprint(esadd(FMIPA,esdir(FMIPA,Solo),esdist(FMIPA,Solo))), sposprint(Solo),


    S 7°34.333' E 110°49.683'
    S 7°34.333' E 110°49.683'

Let us turn to a larger example, Tugu Jogja dan Monas Jakarta (menggunakan Google Earth
untuk mencari koordinatnya).


\>Tugu=[-7.7833°,110.3661°]; Monas=[-6.175°,106.811944°];

\>sposprint(Tugu), sposprint(Monas)


    S 7°46.998' E 110°21.966'
    S 6°10.500' E 106°48.717'

According to Google Earth, the distance is 429.66km. We get a good
approximation.


\>esdist(Tugu,Monas)-\>" km" // perkiraan jarak Tugu Jogja - Monas Jakarta


    Commands must be separated by semicolon or comma!
    Found:  // perkiraan jarak Tugu Jogja - Monas Jakarta (character 32)
    You can disable this in the Options menu.
    Error in:
    esdist(Tugu,Monas)-&gt;" km" // perkiraan jarak Tugu Jogja - Mona ...
                             ^

The heading is the same as the one computed in Google Earth.


\>degprint(esdir(Tugu,Monas))


    294°17'2.85''

However, we do no longer get the exact target position, if we add the
heading and distance to the orginal position. This is so, since we do
not compute the inverse function exactly, but take an approximation of
the earth radius along the path.


\>sposprint(esadd(Tugu,esdir(Tugu,Monas),esdist(Tugu,Monas)))


    S 6°10.500' E 106°48.717'

The error is not large, however.


\>sposprint(Monas),


    S 6°10.500' E 106°48.717'

Of course, we cannot sail with the same heading from one destination
to another, if we want to take the shortest path. Imagine, you fly NE
starting at any point on the earth. Then you will spiral to the north
pole. Great circles do not follow a constant heading!


The following computation shows that we are way off the correct
destination, if we use the same heading during our travel.


\>dist=esdist(Tugu,Monas); hd=esdir(Tugu,Monas);


Now we add 10 times one-tenth of the distance, using the heading to Monas, we got in Tugu.


\>p=Tugu; loop 1 to 10; p=esadd(p,hd,dist/10); end;


The result is far off.


\>sposprint(p), skmprint(esdist(p,Monas))


    S 6°11.250' E 106°48.372'
         1.529km

As another example, let us take two points on the earth at the same
lattitude.


\>P1=[30°,10°]; P2=[30°,50°];


The shortest path from P1 to P2 is not the circle of lattitude 30°,
but a shorter path starting 10° further north at P1.


\>sdegprint(esdir(P1,P2))


         79.69°

But, if we follow this compass reading, we will spiral to the north
pole! So we must adjust our heading along the way. For rough purposes,
we adjust it at 1/10 of the total distance.


\>p=P1;  dist=esdist(P1,P2); ...  
\>     loop 1 to 10; dir=esdir(p,P2); sdegprint(dir), p=esadd(p,dir,dist/10); end;


         79.69°
         81.67°
         83.71°
         85.78°
         87.89°
         90.00°
         92.12°
         94.22°
         96.29°
         98.33°

The distances are not right, since we will add a bit off error, if we
follow the same heading for too long.


\>skmprint(esdist(p,P2))


         0.203km

We get a good approximation, if we adjust out heading after each 1/100 of the total distance
from Tugu to Monas.


\>p=Tugu; dist=esdist(Tugu,Monas); ...  
\>     loop 1 to 100; p=esadd(p,esdir(p,Monas),dist/100); end;

\>skmprint(esdist(p,Monas))


         0.000km

For navigational purposes, we can get a sequence of GPS position along the great circle to
Monas with the function navigate.


\>load spherical; v=navigate(Tugu,Monas,10); ...  
\>     loop 1 to rows(v); sposprint(v[#]), end;


    S 7°46.998' E 110°21.966'
    S 7°37.422' E 110°0.573'
    S 7°27.829' E 109°39.196'
    S 7°18.219' E 109°17.834'
    S 7°8.592' E 108°56.488'
    S 6°58.948' E 108°35.157'
    S 6°49.289' E 108°13.841'
    S 6°39.614' E 107°52.539'
    S 6°29.924' E 107°31.251'
    S 6°20.219' E 107°9.977'
    S 6°10.500' E 106°48.717'

We write a function, which plots the earth, the two positions, and the
positions in between.


\>function testplot ...


    useglobal;
    plotearth;
    plotpos(Tugu,"Tugu Jogja"); plotpos(Monas,"Tugu Monas");
    plotposline(v);
    endfunction
</pre>
Now plot everything.


\>plot3d("testplot",angle=25, height=6,\>own,\>user,zoom=4):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-129.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-129.png)

Or use plot3d to get an anaglyph view of it. This looks really great
with red/cyan glasses.


\>plot3d("testplot",angle=25,height=6,distance=5,own=1,anaglyph=1,zoom=4):


![images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-130.png](images/Hamemayu%20Hayuningrat_23030630053_EMTGeometri-130.png)

# Latihan

1. Gambarlah segi-n beraturan jika diketahui titik pusat O, n, dan jarak titik pusat ke
titik-titik sudut segi-n tersebut (jari-jari lingkaran luar segi-n), r.


Petunjuk:


* 
Besar sudut pusat yang menghadap masing-masing sisi segi-n adalah (360/n).

* 
Titik-titik sudut segi-n merupakan perpotongan lingkaran luar segi-n dan garis-garis yang
* melalui pusat dan saling membentuk sudut sebesar kelipatan (360/n).

* 
Untuk n ganjil, pilih salah satu titik sudut adalah di atas.

* 
Untuk n genap, pilih 2 titik di kanan dan kiri lurus dengan titik pusat.

* 
Anda dapat menggambar segi-3, 4, 5, 6, 7, dst beraturan.


2. Gambarlah suatu parabola yang melalui 3 titik yang diketahui.


Petunjuk:


- Misalkan persamaan parabolanya y= ax^2+bx+c.


- Substitusikan koordinat titik-titik yang diketahui ke persamaan tersebut.


- Selesaikan SPL yang terbentuk untuk mendapatkan nilai-nilai a, b, c.


3. Gambarlah suatu segi-4 yang diketahui keempat titik sudutnya, misalnya A, B, C, D.


   - Tentukan apakah segi-4 tersebut merupakan segi-4 garis singgung (sisinya-sisintya
merupakan garis singgung lingkaran yang sama yakni lingkaran dalam segi-4 tersebut).


   - Suatu segi-4 merupakan segi-4 garis singgung apabila keempat garis bagi sudutnya
bertemu di satu titik.


   - Jika segi-4 tersebut merupakan segi-4 garis singgung, gambar lingkaran dalamnya.


   - Tunjukkan bahwa syarat suatu segi-4 merupakan segi-4 garis singgung apabila hasil kali
panjang sisi-sisi yang berhadapan sama.


4. Gambarlah suatu ellips jika diketahui kedua titik fokusnya, misalnya P dan Q. Ingat
ellips dengan fokus P dan Q adalah tempat kedudukan titik-titik yang jumlah jarak ke P dan
ke Q selalu sama (konstan).


5. Gambarlah suatu hiperbola jika diketahui kedua titik fokusnya, misalnya P dan Q. Ingat
ellips dengan fokus P dan Q adalah tempat kedudukan titik-titik yang selisih jarak ke P dan
ke Q selalu sama (konstan).


