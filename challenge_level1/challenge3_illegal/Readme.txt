# CTB 2023

# Vincent Alleaume

# Challenge_level1 / challenge3_illegal

# first note : i see there is a RVTEST_RV64M definition (not a rv32xx ?),
# that trigger definition of RVTEST_ENABLE_MACHINE 
# at the top of the provided test.S 

# Anyway, after launching the test (using make) :
# plus CTRL-C then Enter for step-by-step, we reach  :

: 
core   0: 0x80000208 (0xfa6292e3) bne     t0, t1, pc - 92
: 
core   0: 0x8000020c (0x341022f3) csrr    t0, mepc
: 
core   0: 0x80000210 (0x30200073) mret
: 
core   0: 0x800001a0 (0x00000000) c.unimp
core   0: exception trap_illegal_instruction, epc 0x800001a0
core   0:           tval 0x00000000

# we encounter an illegal instruction (.word 0). and note such data 
# should be put at the end of the program in dedicated area

# So here i assume fixing the test means: 
# " once the illegal_instruction exception is catched, 
#   make it returning/jumping AFTER the illegal instruction, taking care of alignement also
# so, in the mtvec_handler, let's replace the PC of resume address (from mepc) 
# by the address of 'j fail' instead, located 8 bytes later.
# that is mepc + 8  (as mepc points on '.word 0' address, 
# that reserved 4 bytes).
Launching that modified code seems fine, SPIKE generates its output