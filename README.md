# Program_Counter
module ProgCounter(PC, PC4, PS, in, clock,reset);
	input [63:0] PC4;
	input [1:0] PS; 
	input [63:0]in;
	input clock, reset;
	output reg [63:0] PC;
	
wire load = PS[0] | PS[1];

always @(posedge clock or posedge reset) begin
	if (reset) begin
		PC = 64'd0;
	end
	
	else if (load) begin
	case(PS)
// Program Counter is incremented by four	
		2'b01: PC = PC4 + 64'd4;
	// Program Counter is increment by four plus a specified value
		2'b10: PC = PC4 + 64'd4 + in;
	// Program Counter is increment by four plus a specified value times 4
		2'b11: PC = PC4 + 64'd4 + in*64'd4;	
	endcase
	end
	
	else begin
	// Program Counter is constant
		PC = PC4;
	end
end 

endmodule
