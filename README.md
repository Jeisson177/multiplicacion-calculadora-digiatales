LIBRARY ieee;
USE ieee.std_logic_1164.all;
--------------------------------------------------------------
ENTITY multA_B IS
    PORT (
            swA : IN std_logic_vector (3 DOWNTO 0);
            swB : IN std_logic_vector (3 DOWNTO 0);
            resm: OUT std_logic_vector (7 DOWNTO 0) );
END ENTITY multA_B;
-------------------------------------------------------------
ARCHITECTURE operation OF multA_B IS  
    SIGNAL cin,c1,c2,c3,c4,c5,c6,c7,c8,c9,c10,c11,c12,c13,c14,c15,c16:std_logic; --los carries para cada suma parcial
    SIGNAL m1:std_logic_vector(3 DOWNTO 0);
	 SIGNAL m2:std_logic_vector(4 DOWNTO 0);
    SIGNAL m3:std_logic_vector(5 DOWNTO 0);
    SIGNAL s1:std_logic_vector(5 DOWNTO 0);
	 
    SIGNAL m4:std_logic_vector(6 DOWNTO 0);
	 SIGNAL s2:std_logic_vector(6 DOWNTO 0);
 
    BEGIN  
	cin<='0';	 
    --se multiplica digito por digito
    m1(0)<=swA(0) AND swB(0);
    m1(1)<=swA(0) AND swB(1);
    m1(2)<=swA(0) AND swB(2);
    m1(3)<=swA(0) AND swB(3);
    
	 m2(0)<='0';
    m2(1)<=swA(1) AND swB(0);
    m2(2)<=swA(1) AND swB(1);
    m2(3)<=swA(1) AND swB(2);
    m2(4)<=swA(1) AND swB(3);
	
	 
    m3(0)<='0';
	 m3(1)<='0';
    m3(2)<=swA(2) AND swB(0);
    m3(3)<=swA(2) AND swB(1);
    m3(4)<=swA(2) AND swB(2);
    m3(5)<=swA(2) AND swB(3);

	 m4(0)<='0';
    m4(1)<='0';
	 m4(2)<='0';
    m4(3)<=swA(3) AND swB(0);
    m4(4)<=swA(3) AND swB(1);
    m4(5)<=swA(3) AND swB(2);
    m4(6)<=swA(3) AND swB(3);
   
    -- fin de muliplicacion de digito por digito
    -- se inician sumas parciales 
    
    --m1+m2
       c1<= (m1(0) AND m2(0)) OR  (Cin AND m1(0)) OR (Cin AND m2(0));
    s1(0)<=  m1(0) XOR m2(0);
    
      C2 <= (m1(1) AND m2(1)) OR  (c1 AND m1(1)) OR (c1 AND m2(1));
    s1(1)<=  m1(1) XOR m2(1) XOR c1;
    
       c3<= (m1(2) AND m2(2)) OR  (c1 AND m1(2)) OR (c2 AND m2(2));
    s1(2)<=  m1(2) XOR m2(2) XOR c2;
    
    s1(3)<=  m1(3) XOR m2(3) XOR c3;
	 
    s1(4)<= (m1(3) AND m2(3)) OR  (c1 AND m1(3)) OR (c3 AND m2(3));
	
	 s1(5)<= '0';
    -- s1 + m3
	 
       c5<= (s1(0) AND m3(0)) OR  (Cin AND s1(0)) OR (Cin AND m3(0));
    s2(0)<=  s1(0) XOR m3(0);
    
       c6<= (s1(1) AND m3(1)) OR  (c5 AND s1(1)) OR (c5 AND m3(1));
    s2(1)<=  s1(1) XOR m3(1) XOR c5;
    
       c7<= (s1(2) AND m3(2)) OR  (c6 AND s1(2)) OR (c6 AND m3(2));
    s2(2)<=  s1(2) XOR m3(2) XOR c6;
    
      c8<=  (s1(3) AND m3(3)) OR  (c7 AND s1(3)) OR (c7 AND m3(3));
    s2(3)<=  s1(3) XOR m3(3) XOR c7;
    
       c9<= (s1(4) AND m3(4)) OR  (c8 AND s1(4)) OR (c8 AND m3(4));
	 s2(4)<=  s1(4) XOR m3(4) XOR c8;
	 
	 
	  s2(6)<= (s1(5) AND m3(5)) OR  (c9 AND s1(5)) OR (c9 AND m3(5));
	  s2(5)<=  s1(5) XOR m3(5) XOR c9; 
	 
	 --s2+m4
	 
	     c10<= (s2(0) AND m4(0)) OR  (Cin AND s2(0)) OR (Cin AND m4(0));
    resm(0)<=  s2(0) XOR m4(0);
    
        c11<= (s2(1) AND m4(1)) OR  (c10 AND s2(1)) OR (c10 AND m4(1));
    resm(1)<=  s2(1) XOR m4(1) XOR c10;
    
        c12<= (s2(2) AND m4(2)) OR  (c11 AND s2(2)) OR (c11 AND m4(2));
    resm(2)<=  s2(2) XOR m4(2) XOR c11;
    
        c13<= (s2(3) AND m4(3)) OR  (c12 AND s2(3)) OR (c12 AND m4(3));
    resm(3)<=  s2(3) XOR m4(3) XOR c12;
    
        c14<= (s2(4) AND m4(4)) OR  (c13 AND s2(4)) OR (c14 AND m4(4));
	 resm(4)<=  s2(4) XOR m4(4) XOR c13;
	 
	     c15<= (s2(5) AND m4(5)) OR  (c14 AND s2(5)) OR (c14 AND m4(5));
	 resm(5)<=  s2(5) XOR m4(5) XOR c14;  
	 
	     c16<= (s2(6) AND m4(6)) OR  (c15 AND s2(5)) OR (c15 AND m4(5));
	 resm(6)<=  s2(6) XOR m4(6) XOR c15;
	 
END ARCHITECTURE operation;
--------------------------------------------------------------
