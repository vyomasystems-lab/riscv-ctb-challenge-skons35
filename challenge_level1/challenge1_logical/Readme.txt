# CTB 2023

# Vincent Alleaume

# so, after launching the test (using make) :
# we get 2 'illegal operands' errors :
#
#     test.S: Assembler messages:
#
#     test.S:15855: Error: illegal operands `and s7,ra,z4'
#     test.S:25584: Error: illegal operands `andi s5,t1,s0'

- First error (line 15855) :
>> seems to be the use of an non existing Mnemonic : 
 z4 is not defined in  the ABI Mnemonic.
(Amongst the existing Mnemonic, the closest seems to be s4,
---> so  i "fix" the test by replacing z4 by s4)

- Second error (line 25584):
>> seems to be the use of wrong command type :
'and' is R-Type (and would be ok here), whereas 'andi' is I-type,
and does not match the operands currently provided
---> so i "fix" the test by replacing 'andi' by 'and'
