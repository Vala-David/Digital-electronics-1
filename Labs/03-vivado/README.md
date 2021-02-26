link na repozitář: https://github.com/Vala-David/Digital-electronics-1

1. úkol

2. úkol
```vhdl
architecture Behavioral of mux_2bit_4to1 is
begin
    f_o <= a_i when (sel_i = "00") else 
           b_i when (sel_i = "01") else
           c_i when (sel_i = "10") else
           d_i;

end architecture Behavioral;
```

```vhdl
p_stimulus : process
    begin
        -- Report a note at the begining of stimulus process
        report "Stimulus process started" severity note;


        -- First test values
        s_d <= "00"; s_c <= "00"; s_b <= "00"; s_a <= "00"; 
        s_sel <= "00"; wait for 100 ns;
        
        s_d <= "10"; s_c <= "01"; s_b <= "01"; s_a <= "00"; 
        s_sel <= "00"; wait for 100 ns;
        
        s_d <= "10"; s_c <= "01"; s_b <= "01"; s_a <= "11"; 
        s_sel <= "00"; wait for 100 ns;
        
        s_d <= "10"; s_c <= "01"; s_b <= "01"; s_a <= "00"; 
        s_sel <= "01"; wait for 100 ns;
        
        s_d <= "10"; s_c <= "01"; s_b <= "11"; s_a <= "00"; 
        s_sel <= "01"; wait for 100 ns;
       
        
        -- Report a note at the end of stimulus process
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;

end architecture testbench;
```

3. úkol
```
1.jakmile spustíme program vivado, tak v okně "quick start" klikneme na "create project"
2.otevře se okno s vytvořením projektu a klikneme na "next", v dalším okně zvolíme název projektu a umistění projektu v souborech a dáme "next"
3.zvolíme RTL projekt a "next", v okně "add source" klikneme na tlačítko "create file" a vyjede menší podokno ve kterém zvolíme file type "vhdl" a pojmenujeme soubor  
4.v okně default part zvolíme "boards" a nich najdeme Nexys A7-50T, dále next a finish
5. máme vytvořený tzv. design source

6.pokud chceme přidat tzv. testbech v nabítce klikneme na File -> Add Source a vyjede nám okno
7.vybereme create simulation sources a dáme next 
8.klikneme na create file: File type -> vhdl a pojmenujeme soubor tb_123 a klikneme na finish

9.pokud máme napsaný kod a chceme ho spustit tak úplně vlevo v okně Flow Navigator  najdeme položku Simulation
10.levým talčítkem myši klineme na Run simulation a zvolíme Run Behavioral Simulation
11.simulaci trochu déle trvá než se načte
12.pokud v průběhu načítání simulaci vyskočí např. avast je nutné udělit vyjímku v programu avast na složku kde jsou uložené soubory programu vivado
13.nakonec vám vyskočí okno simulace vašeho kodu
```

