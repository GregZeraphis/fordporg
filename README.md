2.a
Irj olyan assembly programot, ami beolvas, majd letarol 12 szamot.
Ezt kovetoen kiirja a paros szamok osszeget, majd a paratlan szamokat visszafele a beolvasastol szamitva.

extern ki_egesz
extern be_egesz

section .bss
	T : resb 48

section .data
	C : DD 0
	D : DD 0	

section .text
main:
	mov ECX,0
ciklus_eleje:
	cmp ECX,12
	jnb ciklus_vege
	push ECX
	call be_egesz
	pop ECX
	mov DWORD[T+4*ECX],EAX
	inc ECX
	jmp ciklus_eleje
ciklus_vege:

	mov ECX,0
ciklus2_eleje:
	cmp ECX,12
	jnb ciklus2_vege
	mov EAX,DWORD[T+4*ECX]
	DIV 2
	cmp EDX,0
	jne nem_paros
	add C,DWORD[T+4*ECX]
	jmp felt_vege
	nem_paros:
	push DWORD[T+4*ECX]
	inc D
	felt_vege:
	inc ECX
	jmp ciklus2_eleje
ciklus2_vege:
	
	mov ECX, 0
ciklus3_eleje:
	cmp ECX, D
	jnb ciklus3_vege
	pop EAX
	push ECX
	call ki_egesz
	pop ECX
	inc ECX
ciklus3_vege

