# Experiment 2: Blockchain-Based Crowdfunding (Kickstarter Alternative)
## Aim:
To create a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met.

## Algorithm:
1.A project owner starts a campaign with a funding goal and deadline.

2.Contributors can send ETH to the campaign.

3.If the goal is met before the deadline, funds are released to the project owner.

4.If the goal is not met, contributors can withdraw their funds.

## Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Crowdfunding {
    struct Campaign {
        address creator;
        uint256 goal;
        uint256 deadline;
        uint256 amountRaised;
        bool goalMet;
        mapping(address => uint256) contributions;
    }

    Campaign public campaign;

    constructor(uint256 _goal, uint256 _duration) {
        campaign.creator = msg.sender;
        campaign.goal = _goal;
        campaign.deadline = block.timestamp + _duration;
    }

    function contribute() public payable {
        require(block.timestamp < campaign.deadline, "Campaign ended");
        campaign.amountRaised += msg.value;
        campaign.contributions[msg.sender] += msg.value;
    }

    function withdrawFunds() public {
        require(msg.sender == campaign.creator, "Only creator can withdraw");
        require(campaign.amountRaised >= campaign.goal, "Goal not met");
        payable(msg.sender).transfer(campaign.amountRaised);
        campaign.goalMet = true;
    }

    function refund() public {
        require(block.timestamp > campaign.deadline, "Campaign still active");
        require(campaign.amountRaised < campaign.goal, "Goal was met");
        uint256 amount = campaign.contributions[msg.sender];
        campaign.contributions[msg.sender] = 0;
        payable(msg.sender).transfer(amount);
    }
}
```
# Expected Output:
1.Users can contribute ETH to the campaign.

2.If the goal is met, the creator can withdraw funds.

3.If the goal is not met, contributors can claim a refund.


# High-Level Overview:
1.Teaches decentralized fundraising.

2.Avoids fraud by ensuring funds are only transferred if the goal is met.

## Output:
### Output for contribute:
![alt text](<Screenshot 2025-04-20 185501.png>)
### Output for withdraw:
![alt text](<Screenshot 2025-04-20 185352.png>)
### Output for Refund:
![alt text](<Screenshot 2025-04-20 185623.png>)
# RESULT: 
Thus, to create a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met is executed successfully.