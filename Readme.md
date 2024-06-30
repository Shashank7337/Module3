ERC20 Token Smart Contract

This Solidity program is a simple contract that implements the ERC20 token standard. The purpose of the contract is to demonstrate the basic functionality of an ERC20 token, including token creation, transfers, and balance inquiries.

Description

This contract simulates an ERC20 token implementation. ERC20 is a widely adopted standard interface for tokens on the Ethereum blockchain. The contract allows users to create tokens, transfer them to other addresses, and check their token balances.

The contract includes the following key features:
Token creation: Users can create a fixed supply of tokens when deploying the contract.
Token transfers: Users can transfer tokens from their own address to another address.
Balance inquiry: Users can check the token balance of a specific address.
The contract utilizes the ERC20 standard functions, including totalSupply, balanceOf, transfer, and transferFrom, to provide the basic functionality of an ERC20 token.

Getting Started
Executing Program
To run this program, you can use Remix, an online Solidity IDE.

Go to the Remix website at Remix Ethereum IDE.
Click on the "+" icon in the left-hand sidebar to create a new file. Save the file with a .sol extension (e.g., ERC20Token.sol).
Copy and paste the following code into the file:

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
contract MyToken {
    string public name;
    string public symbol;
    uint8 public decimals;
    uint256 public totalSupply;
    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;
    address public owner;
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);
    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can call this function.");
        _;
    }
    constructor(string memory _name, string memory _symbol, uint8 _decimals, uint256 _initialSupply) {
        name = _name;
        symbol = _symbol;
        decimals = _decimals;
        totalSupply = _initialSupply * 10**uint256(decimals);
        balanceOf[msg.sender] = totalSupply;
        owner = msg.sender;
    }
    function transfer(address _to, uint256 _value) external returns (bool) {
        require(_to != address(0) && balanceOf[msg.sender] >= _value, "Invalid recipient or insufficient balance.");
        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;
        emit Transfer(msg.sender, _to, _value);
        return true;
    }
    function approve(address _spender, uint256 _value) external returns (bool) {
        allowance[msg.sender][_spender] = _value;
        emit Approval(msg.sender, _spender, _value);
        return true;
    }
    function transferFrom(address _from, address _to, uint256 _value) external returns (bool) {
        require(_to != address(0) && balanceOf[_from] >= _value && allowance[_from][msg.sender] >= _value, "Invalid recipient, insufficient balance, or insufficient allowance.");
        balanceOf[_from] -= _value;
        balanceOf[_to] += _value;
        allowance[_from][msg.sender] -= _value;
        emit Transfer(_from, _to, _value);
        return true;
    }
    function mint(address _to, uint256 _value) external onlyOwner returns (bool) {
        require(_to != address(0), "Invalid recipient.");
        totalSupply += _value;
        balanceOf[_to] += _value;
        emit Transfer(address(0), _to, _value);
        return true;
    }
    function burn(uint256 _value) external returns (bool) {
        require(balanceOf[msg.sender] >= _value, "Insufficient balance.");
        balanceOf[msg.sender] -= _value;
        totalSupply -= _value;
        emit Transfer(msg.sender, address(0), _value);
        return true;
    }
}
To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.0" (or another compatible version), and then click on the "Compile ERC20Token.sol" button.
Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the ERC20Token contract from the dropdown menu, and then click on the "Deploy" button.
Once the contract is deployed, you can interact with it by calling the transfer function to transfer tokens between addresses. You can also check the token balance of an address using the balanceOf mapping.

Authors

Shashank shekhar 

License

This project is licensed under the MIT License - see the LICENSE.txt file for details.
