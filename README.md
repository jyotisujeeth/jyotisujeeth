- 👋 Hi, I’m @jyotisujeeth
- 👀 I’m interested in fullstack 
- 🌱 I’m currently learning @ sharpener.tech
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me mail me at jyotisujeeth@gmail.com

<!---
jyotisujeeth/jyotisujeeth is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
pragma solidity ^0.5.0;

contract Test {
   address public owner = msg.sender;
   uint public creationTime = now;

   modifier onlyBy(address _account) {
      require(
         msg.sender == _account,
         "Sender not authorized."
      );
      _;
   }
   function changeOwner(address _newOwner) public onlyBy(owner) {
      owner = _newOwner;
   }
   modifier onlyAfter(uint _time) {
      require(
         now >= _time,
         "Function called too early."
      );
      _;
   }
   function disown() public onlyBy(owner) onlyAfter(creationTime + 6 weeks) {
      delete owner;
   }
   modifier costs(uint _amount) {
      require(
         msg.value >= _amount,
         "Not enough Ether provided."
      );
      _;
      if (msg.value > _amount)
         msg.sender.transfer(msg.value - _amount);
   }
   function forceOwnerChange(address _newOwner) public payable costs(200 ether) {
      owner = _newOwner;
      if (uint(owner) & 0 == 1) return;        
   }
}
