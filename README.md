# CAO-ASSIG-01
.data
requestInput: .asciiz "Enter number of disks: "
moveDisk:     .asciiz "Move disk "
fromPeg:      .asciiz " from peg "
newline:      .asciiz "\n"
toPeg:        .asciiz " to peg "
.text
.globl main
main:
       li $v0, 4              
       la $a0, requestInput   
       syscall
       li $v0, 5              
       syscall
       addi $a0, $v0,   0     
       addi $a1, $zero, 1     
       addi $a2, $zero, 2     
       addi $a3, $zero, 3         
       jal  hanoi
       j    Leave
hanoi: addi $sp, $sp, -20            
       sw   $a0, 12($sp)      
       sw   $ra, 16($sp)      
       sw   $a1, 8($sp)       
       sw   $a2, 4($sp)       
       sw   $a3, 0($sp)      
       slti $t0, $a0,   1     
       beq  $t0, $zero, Skip  
       addi $sp, $sp,   20    
       jr   $ra  
Skip:  addi $a0, $a0, -1      
       add  $t0, $a2, $zero   
       add  $a2, $a3, $zero   
       add  $a3, $t0, $zero   
       jal  hanoi                    
       lw   $a3, 0($sp)       
       lw   $a2, 4($sp)       
       lw   $a1, 8($sp)       
       lw   $a0, 12($sp)      
       lw   $ra, 16($sp)      
       addi $sp, $sp, 20      
       add  $t0, $a0, $zero   
       li   $v0, 4            
       la   $a0, moveDisk     
       syscall
       li   $v0, 1            
       add  $a0, $t0, $zero   
       syscall
       li   $v0, 4            
       la   $a0, fromPeg      	
       syscall
       li   $v0, 1            
       add  $a0, $zero, $a1   
       syscall
       li   $v0, 4            
       la   $a0, toPeg        
       syscall
       li   $v0, 1            
       add  $a0, $zero, $a2   
       syscall
