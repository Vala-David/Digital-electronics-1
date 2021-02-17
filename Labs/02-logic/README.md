Cvičení-2

link na repozitář: https://github.com/Vala-David/Digital-electronics-1 

1.úkol

```
2-bit 
|0|00|00|0|1|0|
|1|00|01|0|0|1|
|2|00|10|0|0|1|
|3|00|11|0|0|1|
|4|01|00|1|0|0|
|5|01|01|0|1|0|
|6|01|10|0|0|1|
|7|01|11|0|0|1|
|8|10|00|1|0|0|
|9|10|01|1|0|0|
|10|10|10|0|1|0|
|11|10|11|0|0|1|
|12|11|00|1|0|0|
|13|11|01|1|0|0|
|14|11|10|1|0|0|
|15|11|11|0|1|0|
```

2.úkol




3.úkol

```
4-bit
|0|0000|0000|0|1|0|
|1|0001|0011|0|0|1|
|2|0010|0001|1|0|0|
|3|0110|1100|0|0|1|
|4|0111|0011|1|0|0|
|5|1111|1111|0|1|0|
|6|1001|0001|1|0|0|
|7|1011|1110|0|0|1|
|8|1100|0100|1|0|0|
|9|0011|1100|0|0|1|
```
```
CODE-DESIGN.VHD

entity comparator_2bit is
    port(
        a_i           : in  std_logic_vector(4 - 1 downto 0);

		-- COMPLETE ENTITY DECLARATION
        b_i		      : in  std_logic_vector(4 - 1 downto 0);
        B_greater_A_o : out std_logic;
        B_equals_A_o  : out std_logic;
        

        B_less_A_o    : out std_logic       -- B is less than A
    );
end entity comparator_2bit;

------------------------------------------------------------------------
-- Architecture body for 2-bit binary comparator
------------------------------------------------------------------------
architecture Behavioral of comparator_2bit is
begin
    B_greater_A_o <= '1' when (b_i > a_i) else '0';

    -- WRITE "EQUALS" AND "LESS" ASSIGNMENTS HERE
    B_equals_A_o <= '1' when (b_i = a_i) else '0';
    B_less_A_o   <= '1' when (b_i < a_i) else '0';

end architecture Behavioral;
```
```
CODE-TESTBENCH.VHD

	-- First test values
        s_b <= "0000"; s_a <= "0000"; wait for 100 ns;
        -- Expected output
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        -- If false, then report an error
        report "Test failed for input combination: 0000, 0000" severity error;
        
        -- WRITE OTHER TESTS HERE
		s_b <= "0001"; s_a <= "0011"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0001, 0011" severity error;
        
        s_b <= "0010"; s_a <= "0001"; wait for 100 ns;
        assert ((s_B_greater_A = '1') and (s_B_equals_A = '0') and (s_B_less_A = '0'))
        report "Test failed for input combination: 0010, 0001" severity error;
        
        s_b <= "0110"; s_a <= "1100"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0110, 1100" severity error;
        
        s_b <= "0111"; s_a <= "0011"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0111, 0011" severity error;
        
        s_b <= "1111"; s_a <= "1111"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        report "Test failed for input combination: 1111, 1111" severity error;
        
        s_b <= "1001"; s_a <= "0001"; wait for 100 ns;
        assert ((s_B_greater_A = '1') and (s_B_equals_A = '0') and (s_B_less_A = '0'))
        report "Test failed for input combination: 1001, 0001" severity error;
        
        s_b <= "1011"; s_a <= "1110"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 1011, 1110" severity error;
        
        s_b <= "1100"; s_a <= "0100"; wait for 100 ns;
        assert ((s_B_greater_A = '1') and (s_B_equals_A = '0') and (s_B_less_A = '0'))
        report "Test failed for input combination: 1100, 0100" severity error;
        
        s_b <= "0011"; s_a <= "1100"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0011, 1100" severity error;
```
```
CONSOLE OUTPUT

analyze design.vhd
analyze testbench.vhd
elaborate tb_comparator_2bit
testbench.vhd:51:9:@0ms:(report note): Stimulus process started
testbench.vhd:75:9:@500ns:(assertion error): Test failed for input combination: 0111, 0011
testbench.vhd:99:9:@1us:(report note): Stimulus process finished
Finding VCD file...
./dump.vcd
```
