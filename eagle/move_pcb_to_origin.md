# Move PCB To origin

1) Click "INFO" on the lower border of the PCB for knowing the line starting point (x,y)
2) Take note of first coordinates (FROM x y) - warning: the starting point of the line can be also the second coordinates: check which X value is lower
3) Select the entire PCB with select tool  
4) Remark: Now you consider that, assuming 0,0 is the origin coordinates of the group, you must move the entire PCB of -x and -y relatively to this origin, so..
5) In the command line type MOVE (>0 0)(-x -y)
6) done
