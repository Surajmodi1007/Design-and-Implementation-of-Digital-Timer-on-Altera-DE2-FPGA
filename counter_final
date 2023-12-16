module counter_final(lsb,msb,enable,clock_in,lsb1,msb1,lsb2,msb2,clr,alaram,in_sec,in_min,in_ho);

input clock_in,enable,clr;

input [6:0] in_sec,in_min,in_ho;

reg [6:0] a=7'b0000000,b=7'b0000000,c=7'b0000000;

reg [6:0] reg_sec,reg_min,reg_ho;

output reg [6:0] lsb,msb,lsb1,msb1,lsb2,msb2;

output alaram;
 
reg out=0; 
reg[26:0] counter=27'd0;
parameter DIVISOR = 27'd50000000;
integer i=0;

assign alaram =({reg_ho,reg_min,reg_sec}=={c,b,a})?1:0;


always@(*)
begin

reg_ho=in_ho;
reg_min=in_min;
reg_sec=in_sec;

end

always @(posedge clock_in)
begin
 counter <= counter + 27'd1;
  
 if(counter>=(DIVISOR-1))
  begin
  counter <= 27'd0;
 
 if(enable==1'b1)

begin

a<=a+7'b0000001;

if(a==7'd59)
begin
a<=0;
b<=b+7'b00000001;
end

if(b==7'd59)
begin

b<=0;
c<=c+7'b00000001;

end

if(c==7'd24)
   c<=7'd0;

if(clr==1'b1)
begin
a<=0;
b<=0;
end


seg_lsb(a,lsb);

seg_msb(a,msb);

seg_lsb(b,lsb1);

seg_msb(b,msb1);

seg_lsb(c,lsb2);

seg_msb(c,msb2);
 
 end

 end

 end
 
 

task seg_msb;

input [6:0] a;
output reg [6:0] segment;

begin

case(a/10) 

7'b0000000:segment=7'b0000001;
7'b0000001:segment=7'b1001111;
7'b0000010:segment=7'b0010010;
7'b0000011:segment=7'b0000110;
7'b0000100:segment=7'b1001100;
7'b0000101:segment=7'b0100100;
7'b0000110:segment=7'b0100000;
7'b0000111:segment=7'b0001111;
7'b0001000:segment=7'b0000000;
7'b0001001:segment=7'b0000100;

default segment <= 7'b0000000;

endcase

end

endtask





task seg_lsb;


input [6:0] a;
output reg [6:0] segment;

begin

case(a%10)

0:segment=7'b0000001;
1:segment=7'b1001111;
2:segment=7'b0010010;
3:segment=7'b0000110;
4:segment=7'b1001100;
5:segment=7'b0100100;
6:segment=7'b0100000;
7:segment=7'b0001111;
8:segment=7'b0000000;
9:segment=7'b0000100;

default segment = 7'b0000000;

endcase

end

endtask


/*always#5

begin


if(enable==1'b1)

begin

a<=a+7'b0000001;

if(a==7'd99)
a<=0;


if(clr==1'b1)
a<=0;

seg_lsb(a,lsb);

seg_msb(a,msb);

end

end
*/

endmodule

