// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, Ownable {
    constructor(string memory _name, string memory _symbol, uint256 _initialSupply, address _owner) ERC20(_name, _symbol) Ownable(_owner) {
        _mint(_owner, _initialSupply);
    }

    function mint(address _to, uint256 _value) external onlyOwner returns (bool) {
        _mint(_to, _value);
        return true;
    }

    function burn(uint256 _value) external returns (bool) {
        _burn(msg.sender, _value);
        return true;
    }

function transfer(address _to, uint256 _value) public override returns (bool) {
    _transfer(_msgSender(), _to, _value);
    return true;
}
}
