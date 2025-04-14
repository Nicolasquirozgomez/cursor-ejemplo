use myfood;

DELIMITER $$

CREATE PROCEDURE MostrarPuntajesClientes()
BEGIN
    DECLARE v_cedula INT;
    DECLARE v_puntaje INT;
    DECLARE fin_cursor BOOLEAN DEFAULT FALSE;

    DECLARE cursor_clientes CURSOR FOR
        SELECT cedula, puntaje FROM clientes;

    DECLARE CONTINUE HANDLER FOR NOT FOUND SET fin_cursor = TRUE;

    OPEN cursor_clientes;

    leer_clientes: LOOP
        FETCH cursor_clientes INTO v_cedula, v_puntaje;
        IF fin_cursor THEN
            LEAVE leer_clientes;
        END IF;
        SELECT CONCAT('Cédula: ', v_cedula, ', Puntaje: ', v_puntaje) AS Resultado;
    END LOOP;

    CLOSE cursor_clientes;
END $$

DELIMITER ;

CALL MostrarPuntajesClientes();
