module alu (
    input  wire [31:0] operand_a,     // rs1
    input  wire [31:0] operand_b,     // rs2 or immediate
    input  wire [3:0]  alu_control,   // control signal selecting operation
    output reg  [31:0] result,
    output wire        zero           // flag for BEQ, etc.
);

    // ALU operation encoding
    localparam ALU_ADD  = 4'b0000;
    localparam ALU_SUB  = 4'b0001;
    localparam ALU_AND  = 4'b0010;
    localparam ALU_OR   = 4'b0011;
    localparam ALU_XOR  = 4'b0100;
    localparam ALU_SLL  = 4'b0101;
    localparam ALU_SRL  = 4'b0110;
    localparam ALU_SRA  = 4'b0111;
    localparam ALU_SLT  = 4'b1000;
    localparam ALU_SLTU = 4'b1001;

    wire [4:0] shamt = operand_b[4:0];  // Shift amount from lower bits

    always @(*) begin
        case (alu_control)
            ALU_ADD:  result = operand_a + operand_b;
            ALU_SUB:  result = operand_a - operand_b;
            ALU_AND:  result = operand_a & operand_b;
            ALU_OR:   result = operand_a | operand_b;
            ALU_XOR:  result = operand_a ^ operand_b;
            ALU_SLL:  result = operand_a << shamt;
            ALU_SRL:  result = operand_a >> shamt;
            ALU_SRA:  result = $signed(operand_a) >>> shamt;
            ALU_SLT:  result = ($signed(operand_a) < $signed(operand_b)) ? 32'b1 : 32'b0;
            ALU_SLTU: result = (operand_a < operand_b) ? 32'b1 : 32'b0;
            default:  result = 32'b0;
        endcase
    end

    // Zero flag for branch instructions
    assign zero = (result == 32'b0);

endmodule
