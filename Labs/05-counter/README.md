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

2.úkol

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

3.úkol
```vhdl
entity top is
    Port ( CLK100MHZ : in  STD_LOGIC;
           BTNC      : in  STD_LOGIC;
           SW        : in  STD_LOGIC_VECTOR (1-1 downto 0);
           LED       : out STD_LOGIC_VECTOR (4-1 downto 0);
           CA        : out STD_LOGIC;
           CB        : out STD_LOGIC;
           CC        : out STD_LOGIC;
           CD        : out STD_LOGIC;
           CE        : out STD_LOGIC;
           CF        : out STD_LOGIC;
           CG        : out STD_LOGIC;
           NA        : out STD_LOGIC_VECTOR (8-1 downto 0));
end top;

architecture Behavioral of top is

    signal s_en  : std_logic;
    signal s_cnt : std_logic_vector(4 - 1 downto 0);

begin
    
    clk_en0 : entity work.clock_enable
        generic map(
            g_MAX = > 100000000
        )
        port map(
            clk   => CLK100MHZ,
            reset => BTNC,
            ce_o  => s_en
        );
    
    bin_cnt0 : entity work.cnt_up_down
        generic map(
            g_CNT_WIDTH => 4
        )
        port map(
            clk       => CLK100MHZ,
            reset     =>BTNC,
            en_i      =>s_en,
            cnt_up_i  =>SW(0),
            cnt_o     =>s_cnt
        );

    LED(3 downto 0) <= s_cnt;

    hex2seg : entity work.hex_7seg
        port map(
            hex_i    => s_cnt,
            seg_o(6) => CA,
            seg_o(5) => CB,
            seg_o(4) => CC,
            seg_o(3) => CD,
            seg_o(2) => CE,
            seg_o(1) => CF,
            seg_o(0) => CG
        );
        
    AN <= b"1111_1110";
```


![IMG_20210316_2016465](https://user-images.githubusercontent.com/78855571/111367654-3d340300-8695-11eb-857a-e59e1124678a.jpg)

























