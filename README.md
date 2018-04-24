# Program_Counter
module ProgCounter(PC, PC_in, PS, in, clock,reset);
	input [1:0] PS; 
	input [63:0]in;
	input clock, reset;
	output reg [63:0] PC;
	output [63:0] PC_in;
	
	wire [63:0] PC4 = PC + 64'd4;
	wire load = PS[0] | PS[1];
	
	assign PC_in = PC4;

always @(posedge clock or posedge reset) begin
	if (reset) begin
		PC = 64'd0;
	end
	
	else if (load) begin
	case(PS)
	// Program Counter is incremented by four	
		2'b01: PC = PC4;
	// Program Counter is incremented by a specified value
		2'b10: PC = in;
	// Program Counter is increment by four  plus a specified value times 4
		2'b11: PC = PC4 + in*64'd4;	
	endcase
	end
	
	else begin
	// Program Counter is constant
		PC = PC;
	end
end 

endmodule
