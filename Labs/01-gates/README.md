Cvičení-1

link na repozitář:
https://github.com/Vala-David/Digital-electronics-1


De Morgan's simulation 
```vhdl
architecture dataflow of gates is
begin
    f_o  <= ((not b_i) and a_i) or ((not c_i) and (not b_i));
    fnand_o  <= (a_i nand (not b_i)) nand ((not b_i) nand (not c_i));
    fnor_o <= (a_i nor (not c_i)) nor b_i;

end architecture dataflow;
```
link na vhdl: https://www.edaplayground.com/x/NFdh


Distributive laws simulation
```vhdl
architecture dataflow of gates is
begin
      f1_o <= x_i and (not x_i);
      f2_o <= x_i or (not x_i);
      f3_o <= x_i or  x_i  or  x_i  or  x_i;
      f4_o <= x_i and  x_i  and  x_i  and x_i;
      f11_o <= (x_i and  y_i) or (x_i and  z_i);
      f12_o <= x_i and (y_i or z_i);
      f21_o <= ((x_i or y_i) and (x_i or z_i));
      f22_o <= x_i or (y_i and  z_i);

end architecture dataflow;
```
link na vhdl: https://www.edaplayground.com/x/weMs




