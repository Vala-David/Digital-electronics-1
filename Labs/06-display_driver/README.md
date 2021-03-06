link na repozitář: https://github.com/Vala-David/Digital-electronics-1

1.úkol

![cvik1](https://user-images.githubusercontent.com/78855571/112059121-bd59dd00-8b5b-11eb-9948-c036287c015e.PNG)

2.úkol
```vhdl
p_mux : process(s_cnt, data0_i, data1_i, data2_i, data3_i, dp_i)
    begin
        case s_cnt is
            when "11" =>
                s_hex <= data3_i;
                dp_o  <= dp_i(3);
                dig_o <= "0111";

            when "10" =>
                s_hex <= data2_i;
                dp_o  <= dp_i(2);
                dig_o <= "1011";

            when "01" =>
                s_hex <= data1_i;
                dp_o  <= dp_i(1);
                dig_o <= "1101";

            when others =>
                s_hex <= data0_i;
                dp_o  <= dp_i(0);
                dig_o <= "1110";
        end case;
    end process p_mux;
```
```vhdl
architecture testbench of tb_driver_7seg_4digits is

    constant c_CLK_100MHZ_PERIOD : time    := 10 ns;

    signal s_clk_100MHz  : std_logic;
    signal s_reset       : std_logic;
    
    signal s_data0_i     : std_logic_vector(4 - 1 downto 0);
    signal s_data1_i     : std_logic_vector(4 - 1 downto 0);
    signal s_data2_i     : std_logic_vector(4 - 1 downto 0);
    signal s_data3_i     : std_logic_vector(4 - 1 downto 0);
    signal s_dp_i        : std_logic_vector(4 - 1 downto 0);
    
    signal s_dp_o        : std_logic;
    
    signal s_seg_o       : std_logic_vector(7 - 1 downto 0);
    signal s_dig_o       : std_logic_vector(4 - 1 downto 0);
    
begin
    uut_driver_7seg : entity work.driver_7seg_4digits
        port map(
        clk         => s_clk_100MHz,
        reset       => s_reset,
        
        data0_i     => s_data0_i,
        data1_i     => s_data1_i,
        data2_i     => s_data2_i,
        data3_i     => s_data3_i,
        
        dp_i        => s_dp_i,
        dp_o        => s_dp_o,
        seg_o       => s_seg_o,
        dig_o       => s_dig_o
        );
        
    p_clk_gen : process
    begin
        while now < 750 ns loop       
            s_clk_100MHz <= '0';
            wait for c_CLK_100MHZ_PERIOD / 2;
            s_clk_100MHz <= '1';
            wait for c_CLK_100MHZ_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;

    p_reset_gen : process
    begin
        s_reset <= '0';
        wait for 10ns;
        s_reset <= '1';
        wait for 10ns;
        s_reset <= '0';
        wait;
    end process p_reset_gen;
    
   p_stimulus : process
   begin
       report "Stimulus process started" severity note;
       
       s_data3_i    <= "0011";
       s_data2_i    <= "0001";
       s_data1_i    <= "0100";
       s_data0_i    <= "0010";
       s_dp_i       <= "0111";
       
       report "Stimulus process finished" severity note;
       wait;
   end process p_stimulus;
    
end architecture testbench;
```
![sim](https://user-images.githubusercontent.com/78855571/112058977-8e436b80-8b5b-11eb-9698-6e975198a24b.PNG)

```vhdl
entity top is
     Port ( CLK100MHZ : in  STD_LOGIC;
           BTNC       : in  STD_LOGIC;
           SW         : in  STD_LOGIC_VECTOR (16-1 downto 0);
           
           CA         : out STD_LOGIC;
           CB         : out STD_LOGIC;
           CC         : out STD_LOGIC;
           CD         : out STD_LOGIC;
           CE         : out STD_LOGIC;
           CF         : out STD_LOGIC;
           CG         : out STD_LOGIC;
           
           DP         : out STD_LOGIC; 
           AN         : out STD_LOGIC_VECTOR (8-1 downto 0));   
end top;

architecture Behavioral of top is

begin
    driver_seg_4 : entity work.driver_7seg_4digits
        port map(
            clk        => CLK100MHZ,
            reset      => BTNC,
            
            data0_i(3) => SW(3),
            data0_i(2) => SW(2),
            data0_i(1) => SW(1),
            data0_i(0) => SW(0),
            
            data1_i(3) => SW(7),
            data1_i(2) => SW(6),
            data1_i(1) => SW(5),
            data1_i(0) => SW(4),
            
            data2_i(3) => SW(11),
            data2_i(2) => SW(10),
            data2_i(1) => SW(9),
            data2_i(0) => SW(8),
            
            data3_i(3) => SW(15),
            data3_i(2) => SW(14),
            data3_i(1) => SW(13),
            data3_i(0) => SW(12),
            
            dig_o => AN(4 - 1 downto 0),
            
            seg_o(0) => CA,
            seg_o(1) => CB,
            seg_o(2) => CC,
            seg_o(3) => CD,
            seg_o(4) => CE,
            seg_o(5) => CF,
            seg_o(6) => CG,
            
                        
            dp_i => "0111",
            dp_o => DP
        );
        
        AN(7 downto 4) <= b"1111";

end architecture Behavioral;
```
