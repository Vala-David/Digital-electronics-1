Cvičení-1

link na repozitář:
https://github.com/Vala-David/Digital-electronics-1


De Morgan's simulation, 
link na vhdl:
https://www.edaplayground.com/x/NFdh

```vhdl
architecture dataflow of gates is
begin
    f_o  <= ((not b_i) and a_i) or ((not c_i) and (not b_i));
    fnand_o  <= (a_i nand (not b_i)) nand ((not b_i) nand (not c_i));
    fnor_o <= (a_i nor (not c_i)) nor b_i;

end architecture dataflow;
```

Distributive laws simulation, 
link na vhdl:

```vhdl
```





