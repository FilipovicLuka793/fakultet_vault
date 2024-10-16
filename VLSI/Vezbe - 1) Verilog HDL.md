# Zadatak 1

![[Pasted image 20241016013252.png]]

``` verilog fold title:m21_gate
module m21_gate(I0, I1, S0, Y);
	input I0, I1, S0;
	output Y;
	wire notS0, T0, T1;
	not(notS0, S0);
	and(T0, I1, S0);
	and(T1, I0, notS0);
	or(Y, T0, T1);
endmodule
```

``` verilog fold title:m21_dataflow
module m21_gate(I0, I1, S0, Y);
	input I0, I1, S0;
	output Y;
	assign Y = S0 ? I1 : I0;
endmodule
```

``` verilog fold title:m21_behavioral
module m21_gate(I0, I1, S0, Y);
	input I0, I1, S0;
	output reg Y;
	always @(I0, I1, S0)
		if (S0)
			Y = I1;
		else
			Y = I0;
endmodule
```

Ovde je `{verilog} Y` obelezen kao `{verilog} reg` zato sto je promenljiva.

Kljucna rec `{verilog} always` oznacava da ce uvek da se izvrsava izpocetka linija po liniju. Takodje `{verilog} @()` posle njega znaci da se proverava da li je do neke promene doslo sa vrednostima unutar zagrada. Ako jeste taj blok izvrsiti, ako nije nista se ne radi. 

``` verilog fold title:top_m21_display
module top_m21_display;
	reg i0, i1, s0;
	wire out;
	m21_dataflow m21(.I0(i0), .I1(i1), .S0(s0), .Y(out));
	initial begin
		i0 = 1'b0; 
		i1 = 1'b0; 
		s0 = 1'b0; 
		#10 i0 = 1'b1; 
		#10 s0 = 1'b1; 
		#10 i1 = 1'b1; 
		#10 $stop;
	end
	always @(out)
		$display("Vreme = %0d, Izlaz = %d", $time, out);
endmodule
```

Blok `{verilog} initial` oznacava da ce taj blok inicialno da se izvrsi.

Sintaksa `{verilog} 1'b0` je sledeca:
* 1 - predstavlja broj bita
* b - predstavlja u kakvo broju je rec (binarnom - b, heksadecimalnom - h, decimalnom - d)
* 0 - vrednost koja treba da se dodeli

`{verilog} #10` predstavlja koliko se taktova ceka dok se ne izvrsi ta linija.

Komanda `{verilog} $display` radi slicno kao i `{cpp} std::cout` u c++.

``` verilog fold title:top_m21_monitor
module top_m21_monitor;
	reg i0, i1, s0; 
	wire out; 
	m21_behavioral m21(.I0(i0), .I1(i1), .S0(s0), .Y(out)); 
	initial begin
		$monitor("Vreme = %2d, Izlaz = %d", $time, out); 
		i0 = 1'b0; 
		i1 = 1'b0; 
		s0 = 1'b0; 
		#10 i0 = 1'b1; 
		#10 s0 = 1'b1; 
		#10 i1 = 1'b1; 
		#10 $finish; 
	end 
endmodule
```

Kljucna rec `{verilog} $monitor` ima istu ulogu kao i `{verilog} $display` samo sto ona se poziva uveka kada se promeni promenljiova `{verilog} out`.

# Zadatak 2

![[Pasted image 20241016125406.png]]
``` verilog fold title:m21_enable
module m21_enable( 
	input I0, 
	input I1, 
	input S0, 
	input E, 
	output Y 
); 
	wire notS0, T0, T1; 
	not(notS0, S0); 
	and(T0, I1, S0, E); 
	and(T1, I0, notS0, E); 
	or(Y, T0, T1); 
endmodule
```

``` verilog fold title:top_m21
module top_m21; 
	reg i [1:0], s0, e; 
	wire out; 
	integer index; 
	m21_enable m21(.I0(i[0]), .I1(i[1]), .S0(s0), .E(e), .Y(out)); 
	initial begin 
		$monitor("Vreme = %2d, Izlaz = %d", $time, out); 
		for (index = 0; index < 2; index = index + 1) 
			i[index] = 1'b0; 
		s0 = 1'b0; 
		e = 1'b0; 
		#10 i[0] = 1'b1;
		#10 s0 = 1'b1; 
		e = 1'b1; 
		#10 i[1] = 1'b1; 
		#10 $finish; 
	end 
endmodule
```

Novina ovde je sto input signali `{verilog} i0` i `{verilog} i1` mogu da se zapisu u obliku niza `{verilog}i [1:0]`.

# Zadatak 3

![[Pasted image 20241016130148.png]]
``` verilog fold title:m41_behavioral
module m41_behavioral(I0, I1, I2, I3, S, Y); 
	input I0, I1, I2, I3; 
	input [1:0] S; 
	output reg Y; 
	always @(I0 or I1 or I2 or I3 or S) 
		case (S) 
			2'b00: Y = I0; 
			2'b01: Y = I1; 
			2'b10: Y = I2; 
			2'b11: Y = I3; 
		endcase 
endmodule
```

Ovde se uvodi sintaksa `{verilog}[1:0] S` koja NIJE niz vec je objekat `{verilog}S` koji ima 2 bita. Ovakav zapis `{verilog}S[1:0]` bi znacio da ima 2 objekta `{verilog}S`, a zapis `{verilog}[1:0] S [2:0]` bi znacio da postoje 3 objekta `{verilog}S` koji se sastoje od 2 bita.

Takodje u ovom primeru se uvodi kljucna rec `{verilog} case` koja se koristi slicno kao i u ostalim jezicima.

``` verilog fold title:top_m41_always
module top_m41_always; 
	reg i0, i1, i2, i3; 
	reg [1:0] s;
	// reg s0, s1; 
	wire out; 
	m41_behavioral m41(i0, i1, i2, i3, s, out);
	// m41_behavioral m41(i0, i1, i2, i3, {s1, s0}, out);  
	initial begin 
		i0 = 1'b0; 
		i1 = 1'b0; 
		i2 = 1'b0; 
		i3 = 1'b0; 
		s = 2'b00; 
		#320 $finish; 
	end 
	always #5 i0 = ~i0; 
	always #10 i1 = ~i1; 
	always #20 i2 = ~i2; 
	always #40 i3 = ~i3; 
	always #80 s[0] = ~s[0]; 
	always #160 s[1] = ~s[1]; 
endmodule
```

# Zadatak 4

![[Pasted image 20241016131448.png]]

``` verilog fold title:cd42
module cd42(I, Y, W); 
	input [3:0] I; 
	output reg [1:0] Y; 
	output reg W; 
	always @(I) 
		casex (I) 
			4'b0001: begin Y = 2'b00; W = 1'b1; end 
			4'b001x: begin Y = 2'b01; W = 1'b1; end 
			4'b01xx: begin Y = 2'b10; W = 1'b1; end 
			4'b1xxx: begin Y = 2'b11; W = 1'b1; end 
			default: begin Y = 2'b00; W = 1'b0; end 
		endcase 
endmodule
```

`{verilog}casex` funkcionise kao `{verilog}case` samo sto mozemo da koristimo `{verilog}x` kao dzoker znak koji znaci da moze bilo koja vrednost da bude postavljena. Tako da `{verilog}4'b1xxx` znaci da vrednost `{verilog}I` pocinje sa 1 a ostale 3 cifre mogu da budu bilo sto.

``` verilog fold title:top_cd42
module top_cd42; 
	reg [3:0] i; 
	wire [1:0] out; 
	wire w; 
	cd42 priority_encoder(.I(i), .Y(out), .W(w)); 
	initial begin
		$monitor("Vreme = %2d, Izlaz = %b, W = %d", $time, out, w); 
		i = 4'b0000; 
		#10 i = 4'b1111; 
		#10 i = 4'b0101; 
		#10 i = 4'b0010; 
		#10 i = 4'b0001; 
		#10 $finish; 
	end  
endmodule
```

# Zadatak 5

![[Pasted image 20241016132114.png]]

