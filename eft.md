# POS Environment and EFT Terminal Penetration Testing Checklist
### This checklist for high-level test focus areas and can be used necessarily for test planning.

## Focus Area 1 - Test reading of card in EFT Terminal
- [ ] 1.	Could the EFT-terminal be exploited by triggering different type of payment methods? <br>
	- [ ] a.	Mag stripe tested <br>
	- [ ] b.	Chip tested <br>
	- [ ] c.	NFC tested <br>
	- [ ] d.	Refund <br>
	- [ ] e.	Fallback method tested <br>
- [ ] 2.	When card payment authorizations are being performed and visualized on the EFT-terminal, what happens when the card is removed intentionally?

## Focus Area 2 - Information from the EFT device
#### Recommendation is to do this test as the last test to not break the terminal.
- [ ] 1.	When information is displayed on the EFT-terminal, could this type of information be useful when trying to exploit the EFT-terminal? <br>
- [ ] 2.	Verify if default passwords are used and what you can do bypassing the password prompt, if possible. As an example, can you lower the security or access card data? <br>
- [ ] 3.	Is it possible to perform parameter / software updates as non-admin user?

## Focus Area 3 - Connections on the EFT device
- [ ] 1.	Examine the physical ports. Can you mount to access log files etc. <br>
- [ ] 2.	Do a port scan on the EFT if connected to an Ethernet cable.

## Focus Area 4 – Connection between EFT and ECR
- [ ] 1.	Investigate the communication between EFT and ECR. <br>
- [ ] 2.	Receipt information is usually sent unencrypted. Any card data visible here? Card data should be truncated/masked. <br>
- [ ] 3.	Some encrypted data should also be seen, if payments go via ECR. Investigate the encryption of this data.

## Focus Area 5 – Data stored in memory & storage on the ECR
- [ ] 1.	Search the memory and logs of the ECR for card data for all supported payment methods <br>
	- [ ] a.	Verify logs and memory for Mag Stripe <br>
	- [ ] b.	Verify logs and memory NFC <br>
	- [ ] c.	Verify logs and memory Chip <br>
	- [ ] d.	Verify logs and memory Refund <br>
- [ ] 2.	Do a port scan of the ECR if EFT Communication to host goes via ECR, unnecessarily ports should not be open.

## Focus Area 6 – Data transferred to and from the EFT server
#### Man in the middle. Note, do not perform any test against the host.
  - [ ] a.	Can you break line encryption? <br>
	- [ ] b.	Is line encryption same as document states? <br>
	- [ ] c.	Is data field encryption same as document states? <br>
	- [ ] d.	What ciphers does the EFT support? (If line encryption is activated at ECR, check ECR) <br>
	- [ ] e.	What cipher is selected?

