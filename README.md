# MIPS_Processor_Datapath

+ IF(Instruction Fetch)
+ ID(Instruction Decode, Register File Read)
+ EX(Execute, Address Calculation)
+ MEM(Memory Access)
+ WB(Write Back)

![Datapath](https://user-images.githubusercontent.com/64410393/108399917-fef62000-725d-11eb-8d44-14a0fff01240.JPG)



---
일단 Register Read는 rs, rt 레지스터 번호가 두개 입력이 되면  
그것의 데이터 값을 전역으로 선언된 read data 값에 넣어주는 역할을 하였습니다.  
또한 Control_Signal은 일단 어떤 opcode인가에 따라 controler의 값을 모두 초기화 해주는 역할을 하였습니다.  
ALU_control_Signal은 ALUop에 따라서 ALU제어에 어떤 연산을 수행하는지에 대한 구분을 해주었고,  
차후에 ALU_func에 그 연산결과의 control input값을 넣어서 그것에 따라 연산을 실행할 수 있도록 코드를 짰습니다.  
Memory_Access는 아까 opcode에 초기화된 MemWrite와 MemRead MUX의 control 값에 의하여 타입별로 리턴값을 반환하도록 하였습니다.  
그 전에 MUX는 시그널 0,1에 따라 아웃풋을 어떤 아웃풋을 내는지에 대한 함수로 만들었습니다.  
또한, Register_Write에서는 이 값을 레지스터에 저장할지 저장하지 않을지에 대해서 결정해야하기 때문에,
RegWrite MUX와 만약 레지스터가 저장되야한다면 RegDst을 통해 저장할 장소를 정하고 아까 Memory Result값을 넣어줄 수 있도록 코딩하였습니다.  
이렇게 ADD연산을 완성하니 LW와 SW는 Control_Signal 함수의 control값을 초기화하는 것과 Memory_Access와 같이 다른 함수들을 조금씩 수정하여 Datapath를 완성하였습니다.

J연산은 일단 점프 control이 어떤식으로 사용이 되는지에 대해 먼저 생각을 하였고 일단 점프 연산이 수행이 된다면 그 control 값으로 shift 2값과 pc+4를 더한 값을 반환하였습니다. 또한 Beq도 Branch control값과 이전의 ALU과정에서 zero의 역할이 수행되었다면 그거에 따라 반환해야하는 주소 값을 만들어서 MUX를 사용해 점프와 Beq의 결과값을 구분할 수 있도록 하였습니다. 
