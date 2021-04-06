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

![IMG_20210406_1105513](https://user-images.githubusercontent.com/78855571/113687220-63632680-96c8-11eb-9697-856e77506ad0.jpg)

```vhdl
p_traffic_fsm : process(clk)
    begin
        if rising_edge(clk) then
            if (reset = '1') then      
                s_state <= STOP1 ;      
                s_cnt   <= std_logic_vector(c_ZERO);     

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
```vhdl
p_output_fsm : process(s_state)
    begin
        case s_state is
            when STOP1 =>
                south_o <= "100";   
                west_o  <= "100";   
                
            when WEST_GO =>
                south_o <= "100";  
                west_o  <= "010";   
                
            when WEST_WAIT =>
                south_o <= "100";   
                west_o  <= "110";   
            
            when STOP2 =>
                south_o <= "100";  
                west_o  <= "100";  
                
            when SOUTH_GO =>
                south_o <= "010";  
                west_o  <= "100";   
                
            when SOUTH_WAIT =>
                south_o <= "110";  
                west_o  <= "100";                   

            when others =>
                south_o <= "100";  
                west_o  <= "100";  
        end case;
    end process p_output_fsm;
```

3.úkol

|State     |South |West  |Delay|
|----------|------|------|-----|
|STOP1     |red   |red   |1s   |
|WEST_GO   |red   |green |4s   |
|WEST_WAIT |red   |yellow|2s   |
|STOP2     |red   |red   |1s   |
|SOUTH_GO  |green |red   |4s   |
|SOUTH_WAIT|yellow|red   |2s   |

![IMG_20210406_1105598](https://user-images.githubusercontent.com/78855571/113687253-6bbb6180-96c8-11eb-87cf-6eec72278a94.jpg)

```vhdl
p_traffic_fsm : process(clk)
    begin
        if rising_edge(clk) then
            if (reset = '1') then      
                s_state <= STOP1 ;    
                s_cnt   <= std_logic_vector(c_ZERO);      

            elsif (s_en = '1') then
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
                            if (sens_w = '1' and sens_s = '0') then  
                                s_state <= WEST_GO;
                            else
                                s_state <= WEST_WAIT;
                            end if;
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
                            if (sens_w = '0' and sens_s = '1') then  
                                s_state <= SOUTH_GO;
                            else
                                s_state <= SOUTH_WAIT;
                            end if;
                            
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


