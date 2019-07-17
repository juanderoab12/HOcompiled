Escriban qué esperan de cada uno de los pasos
1. Escriban qué esperan de cada uno de los pasos

	1) precomp -> El codigo verifica si esta todo bien con la escritura, optimza el codigo, 
	2) comp1 -> traduce el codigo que uno le asigna a lenguaje assemble
	3) comp2 -> de lenguaje assemble lo pasa a lenguaje maquina
	4) linkeo -> determina que linkeo se necesitara al momento de compilar

2. ¿Qué agregó el preprocesador?
	derifica que la escritura este bien y que lo declarado se encuentra definido en los includes del archivo a compilar
3. Identificar en la rutina de assembler las funciones


        .file   "calculator.c"
        .section        .rodata   /////////// la aplicacion es capaz de leer la informacion (read only) 
        .align 8
.LC0:
        .string "I know how to add! 31 + 11 is %d\n"  ////   printf("I know how to add! 31 + 11 is %d\n", sum);
        .text
        .globl  main			//// esta dentro del main de c
        .type   main, @function		//// en ese main esta una funcion 
main:
.LFB0:
        .cfi_startproc
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset 6, -16
        movq    %rsp, %rbp
        .cfi_def_cfa_register 6
        subq    $32, %rsp
        movl    %edi, -20(%rbp)
        movq    %rsi, -32(%rbp)
        movl    $11, %esi
        movl    $31, %edi
        call    add_numbers			/// llama a la funcion add_number
        movl    %eax, -4(%rbp)
        movl    -4(%rbp), %eax
        movl    %eax, %esi
        movl    $.LC0, %edi
        movl    $0, %eax
        call    printf				/// llama la funcion printf 
        movl    $0, %eax			/// devuelve valor 0 ?
        leave
        .cfi_def_cfa 7, 8
        ret
        .cfi_endproc
.LFE0:
        .size   main, .-main
        .globl  add_numbers 			/// int add_numbers (declarada la funcion) 
        .type   add_numbers, @function		/// describe que tipo de la funcion 
add_numbers:					/// describe como se realizara la suma 
.LFB1:
        .cfi_startproc
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset 6, -16
        movq    %rsp, %rbp
        .cfi_def_cfa_register 6
        movl    %edi, -4(%rbp)
        movl    %esi, -8(%rbp)
        movl    -4(%rbp), %edx
        movl    -8(%rbp), %eax
        addl    %edx, %eax
        popq    %rbp
        .cfi_def_cfa 7, 8
        ret
        .cfi_endproc
.LFE1:
        .size   add_numbers, .-add_numbers
        .ident  "GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.10) 5.4.0 20160609"
        .section        .note.GNU-stack,"",@progbits


4. Explicar qué quieren decir los símbolos que se crean en el objeto
	Es la traduccion del codigo de c que paso por assemble antes de llegar a  lenguaje maquina, el objeto es binario pero aun no se ejecutaria porque no tiene detemrinados los linkers	

5. ¿En qué se diferencian los símbolos del objeto y del ejecutable?
	el ejecutable ya tiene designado los linkers que va a buscar para su ejecucion, en cambio el los del objeto no presentan los linkers 	

