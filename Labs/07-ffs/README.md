link na repozitář: https://github.com/Vala-David/Digital-electronics-1

1.úkol:

|D|Q|Q(n+1)|Change|
|-|-|------|------|
|0|0|0     |No    |
|0|1|0     |Yes   |
|1|1|1     |No    |
|1|0|1     |Yes   |

|J|K|Qn|Q(n+1)|Change|
|-|-|--|------|------|
|0|0|0 |0     |No    |
|0|0|1 |1     |No    |
|0|1|0 |0     |Reset |
|0|1|1 |0     |Reset |
|1|0|0 |1     |Set   |
|1|0|1 |1     |Set   |
|1|1|0 |1     |Toggle|
|1|1|1 |0     |Toggle|

|T|Qn|Q(n+1)|Change|
|-|--|------|------|
|0|0 |0     |No    |
|0|1 |1     |No    |
|1|0 |1     |Toggle|
|1|1 |0     |Toggle|

2.úkol
```vhdl
p_d_latch : process(en, d, arst)
    begin
        if (arst = '1') then
            q <= '0';
            q_bar <= '1';
        elsif (en = '1') then
            q <= d;
            q_bar <= not d;
    end if;
    end process p_d_latch;
```
```vhdl
p_stimulus : process
    begin

        report "Stimulus process started" severity note;
        
        s_en    <= '0';
        s_arst  <= '0';
        s_d     <= '0';
        wait for 10 ns; 
        s_arst  <= '1'; 
        wait for 10 ns;
        s_arst  <= '0'; 
        
        s_d    <= '1';
        wait for 10ns;
        assert (s_q = '0' and s_q_bar = '1');
        s_d    <= '0';
        wait for 10ns;
        assert (s_q = '0' and s_q_bar = '1');
        
        s_en   <= '1';
        s_d    <= '1';
        wait for 10ns;
        assert (s_q = '1' and s_q_bar = '0');
        s_en   <= '1';
        s_d    <= '0';
        wait for 10ns;
        assert (s_q = '0' and s_q_bar = '1');
        
        s_en   <= '1';
        s_d    <= '1';
        wait for 10ns;
        s_arst <= '1';
        assert (s_q = '0' and s_q_bar = '1')
        report "Stimulus process end" severity note;
        wait;
        
    end process p_stimulus;
```
![sim d_latch](https://user-images.githubusercontent.com/78855571/112806493-1bfcea80-9077-11eb-9fe1-53e6ec39b356.png)

3.úkol

a)
```vhdl
p_d_ff_arst : process(clk, arst)
    begin
        if (arst = '1') then
            q <= '0';
            q_bar <= '1';
        elsif rising_edge(clk) then
            q <= d;
            q_bar <= not d;
    end if;
    end process p_d_ff_arst;
```
```vhdl
```






