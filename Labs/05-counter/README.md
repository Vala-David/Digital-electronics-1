link na repozitář: https://github.com/Vala-David/Digital-electronics-1

1.úkol

|Time interval|Number of clk periods|Number of clk periods in hex|Number of clk periods in binary            |
|-------------|---------------------|----------------------------|-------------------------------------------|
|    2 ms     |     200 000         |      x"3_0D40"             |   b"0011_0000_1101_0100_0000"             |
|    4 ms     |     400 000         |      x"6_1A80"             |   b"0110_0001_1010_1000_0000"             |
|   10 ms     |     1 000 000       |      x"F_4240"             |   b"1111_0100_0010_0100_0000"             |
|   250 ms    |     25 000 000      |      x"17D_7840"           |   b"0001_0111_1101_0111_1000_0100_0000"   |
|   500 ms    |     50 000 000      |      x"2FA_F080"           |   b"0010_1111_1010_1111_0000_1000_0000"   |
|    1 sec    |     100 000 000	    |      x"5F5_E100"           |   b"0101_1111_0101_1110_0001_0000_0000"   |

2. úkol

```vhdl
begin
    p_cnt_up_down : process(clk)
    begin
        if rising_edge(clk) then
        
            if (reset = '1') then               
                s_cnt_local <= (others => '0'); 

            elsif (en_i = '1') then       

                s_cnt_local <= s_cnt_local + 1;

            end if;
        end if;
    end process p_cnt_up_down;

    cnt_o <= std_logic_vector(s_cnt_local);

end architecture behavioral;
```

```vhdl
    p_reset_gen : process
    begin
        s_reset <= '0';
        wait for 12 ns;

        s_reset <= '1';
        wait for 73 ns;

        s_reset <= '0';
        wait;
    end process p_reset_gen;

    p_stimulus : process
    begin
        report "Stimulus process started" severity note;

        s_en     <= '1';
        
        s_cnt_up <= '1';
        wait for 380 ns;
        s_cnt_up <= '0';
        wait for 220 ns;

        s_en     <= '0';

        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;

end architecture testbench;
```
![cnt_up_down_sim](https://user-images.githubusercontent.com/78855571/111025307-8e1cd080-83e3-11eb-917e-23f4e9524d6c.png)

