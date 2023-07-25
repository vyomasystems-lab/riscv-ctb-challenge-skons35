# CTB 2023

# Vincent Alleaume

# Challenge_level1 / challenge2_loop

# so, after launching the test (using make) :
# we get stuck in a loop, because of a bad condition check
# to know when quitting that loop :
#  -> after 3 succesfull tests here, we end the test
#  -> if a test fails, we quit immediately after that bad test
# (test being computing sum of 1st word + 2nd word, and comparing to 3rd word)

# so i propose to change the end of test detection using
#  the t5 register that is initialized with number of tests (but not used yet)

# here is the fixed resulting code (loop part only, plus commented lines) :
....

loop:
	lw t1, (t0)
  lw t2, 4(t0)
  lw t3, 8(t0)
  add t4, t1, t2
  addi t0, t0, 12
  # beq t3, t4, loop        # check if sum is correct
  # j fail
  bne t3, t4, fail         # immediate quit on incorrect sum
  # need to know when to stop the tests (so use t5 that contains tests count)
  addi t5, t5, -1
  bne t5, x0, loop   # do we have more test to do ?

test_end:
....