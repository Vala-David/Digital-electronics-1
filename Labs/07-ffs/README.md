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
TESTBENCH
```vhdl
p_reset_gen : process
        begin
            s_arst <= '0';
            wait for 12 ns;
            s_arst <= '1';
            wait for 30 ns;
            s_arst <= '0';
            wait;
        end process p_reset_gen;
```
```vhdl
p_stimulus : process
        begin
            report "Stimulus process started" severity note;
            s_d <= '1';
            wait for 10ns;
            assert (s_q = '0' and s_q_bar = '1');
            s_d <= '0';
            wait for 10ns;
            assert (s_q = '0' and s_q_bar = '1');
            s_d <= '1';
            wait for 10ns;
            assert (s_q = '1' and s_q_bar = '0');
            s_d <= '0';
            wait for 10ns;
            assert (s_q = '0' and s_q_bar = '1');
            wait for 20ns;
            s_d <= '1';
            wait for 10ns;
            assert (s_q = '0' and s_q_bar = '1');
            report "Stimulus process ended" severity note;
            wait;
        end process p_stimulus;
```
![sim d_ff_latch](https://user-images.githubusercontent.com/78855571/112815321-7a7a9680-9080-11eb-98cb-d608556a423e.png)

b)
```vhdl
p_d_ff_arst : process(clk)
    begin
        if rising_edge(clk) then
        if (rst = '1') then
            q <= '0';
            q_bar <= '1';
        else
            q <= d;
            q_bar <= not d;
        end if;
        end if;
    end process p_d_ff_arst;
```
TESTBENCH
```vhdl
p_clk_gen : process
    begin
        while now < 750 ns loop
            s_clk <= '0';
            wait for c_CLK_100MHZ_PERIOD / 2;
            s_clk <= '1';
            wait for c_CLK_100MHZ_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;
```
```vhdl
p_reset_gen : process
    begin
        s_arst  <= '0';
        wait for 12 ns;
        s_arst  <= '1'; 
        wait for 30 ns;
        s_arst  <= '0';
        wait;
    end process p_reset_gen;
```
```vhdl
p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        s_d <= '1';
        wait for 10ns;
        assert (s_q = '1' and s_q_bar = '0');
        s_d <= '0';
        wait for 10ns;
        assert (s_q = '0' and s_q_bar = '1');
        s_d <= '1';
        wait for 10ns;
        assert (s_q = '0' and s_q_bar = '1');
        s_d <= '0';
        wait for 10ns;
        assert (s_q = '0' and s_q_bar = '1'); 
        wait for 20ns;
         s_d <= '1';
        wait for 25ns;
        assert (s_q = '1' and s_q_bar = '0');
        report "Stimulus process ended" severity note;
        wait;
    end process p_stimulus;
```





