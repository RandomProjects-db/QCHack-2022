    '''
    CNOT gate to flip the second Qubit conditonally
    on the first qubit being in the state |1⟩
    '''
    CNOT | (qubit_one, qubit_two)

    return qubit_one, qubit_two


'''
The create_message function takes one of the entangled qubits as a input, 
and a message value. The message value is a bit with the value of 0 or 1. 
The message_value is then entangled with the qubit, and converted into 
two classical bits to send the data through classical channels
'''

    # entangle the original qubit with the message qubit
    CNOT | (qubit_to_send, qubit_one)

    '''
    1 - Put the message qubit in superposition 
    2 - Measure out the two values to get the classical bit value
        by collapsing the state. 
    '''
    H | qubit_to_send
    Measure | qubit_to_send
    Measure | qubit_one

    # The qubits are now turned into normal bits we can send through classical channels
    classical_encoded_message = [int(qubit_to_send), int(qubit_one)]

    return classical_encoded_message


'''
The function to receive messages takes the classical encoded
message, along with the second qubit from the Bell pair. 
Then Pauli-X and/or Pauli-Z gates are applied to the Qubit,
conditionally on the values in the message. 
'''

    '''
    Pauli-X and/or Pauli-Z gates are applied to the Qubit,
    conditionally on the values in the message.
    '''
    if message[1] == 1:
        X | qubit_two
    if message[0] == 1:
        Z | qubit_two

    '''
    Measuring the Qubit and collapsing the state down to either 1 or 0
    '''
    Measure | qubit_two

    quantum_engine.flush()

    received_bit = int(qubit_two)
    return received_bit


    '''
    The binary message is divided into an list of each word represented in binary.
    We iterate through each word, and then each bit in the letter.
    Then we append the bits to an list to get back the letter representation
    '''

