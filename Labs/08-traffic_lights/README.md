link na repozitář: https://github.com/Vala-David/Digital-electronics-1

1.úkol

|Input P|Clock|State|Output R|
|-------|-----|-----|--------|
|0      |↑    |A    |0       |
|0      |↑    |A    |0       |
|1      |↑    |B    |0       | 
|1      |↑    |C    |0       |
|0      |↑    |C    |0       | 
|1      |↑    |D    |1       | 
|0      |↑    |A    |0       | 
|1      |↑    |B    |0       |
|1      |↑    |C    |0       | 
|1      |↑    |D    |1       | 
|1      |↑    |B    |0       | 
|0      |↑    |B    |0       | 
|0      |↑    |B    |0       | 
|1      |↑    |C    |0       | 
|1      |↑    |D    |1       | 
|1      |↑    |B    |0       | 

|RGB LED|Pin name   |Red  |Yellow|Green|
|-------|--------   |-----|------|-----|
|LD16   |N15,M16,R12|1,0,0|1,1,0 |0,1,0|
|LD17   |N16,R11,G14|1,0,0|1,1,0 |0,1,0|

2.úkol
```vhdl
p_traffic_fsm : process(clk)
    begin
        if rising_edge(clk) then
            if (reset = '1') then       -- Synchronous reset
                s_state <= STOP1 ;      -- Set initial state
                s_cnt   <= std_logic_vector(c_ZERO);      -- Clear all bits

            elsif (s_en = '1') the
                case s_state is
                
                    when STOP1 =>
                        if (unsigned(s_cnt) < c_DELAY_1SEC) then
                            s_cnt <= std_logic_vector(unsigned(s_cnt) + 1);
                        else
                            s_state <= WEST_GO;
                            s_cnt   <= std_logic_vector(c_ZERO);
                        end if;

                    when WEST_GO =>
                        if (unsigned(s_cnt) < c_DELAY_4SEC) then
                            s_cnt <= std_logic_vector(unsigned(s_cnt) + 1);
                        else
                            s_state <= WEST_WAIT;
                            s_cnt   <= std_logic_vector(c_ZERO);
                        end if;
                        
                    when WEST_WAIT =>
                        if (unsigned(s_cnt) < c_DELAY_2SEC) then
                            s_cnt <= std_logic_vector(unsigned(s_cnt) + 1);
                        else
                            s_state <= STOP2;
                            s_cnt   <= std_logic_vector(c_ZERO);
                        end if;
                        
                    when STOP2 =>
                        if (unsigned(s_cnt) < c_DELAY_1SEC) then
                            s_cnt <= std_logic_vector(unsigned(s_cnt) + 1);
                        else
                            s_state <= SOUTH_GO;
                            s_cnt   <= std_logic_vector(c_ZERO);
                        end if;
                        
                    when SOUTH_GO =>
                        if (unsigned(s_cnt) < c_DELAY_4SEC) then
                            s_cnt <= std_logic_vector(unsigned(s_cnt) + 1);
                        else
                            s_state <= SOUTH_WAIT;
                            s_cnt   <= std_logic_vector(c_ZERO);
                        end if;
                        
                    when SOUTH_WAIT =>
                        if (unsigned(s_cnt) < c_DELAY_2SEC) then
                            s_cnt <= std_logic_vector(unsigned(s_cnt) + 1);
                        else
                            s_state <= STOP1;
                            s_cnt   <= std_logic_vector(c_ZERO);
                        end if;
                    
                    when others =>
                        s_state <= STOP1;

                end case;
            end if; 
        end if; 
    end process p_traffic_fsm;
```
