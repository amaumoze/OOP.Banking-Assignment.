# OOP.Banking-Assignment.class Bank(object):
    def __init__(self, Bank_Id, Bankname, Location):
        self.Bank_Id = Bank_Id
        self.Bankname = Bankname
        self.Location = Location


class CustomerMenu(Bank):
    def __init__(self,Bank_Id, Bankname, Location, Customer_Id, AccountNo, Name, Address, PhoneNo):
        super(Customer, self).__init__(Bank_Id, Bankname, Location)
        self.accounts = {}
        self.Customer_Id = Customer_Id
        self.AcctNo = AccountNo
        self.Name = Name
        self.Address = Address
        self.PhoneNo = PhoneNo

    def GeneralInquiry(self):
        try:
            w1 = self.accounts[self.Customer_Id]['Customer_Id']
            w2 = self.accounts[self.Customer_Id]['Name']
            w3 = self.accounts[self.Customer_Id]['Address']
            w4 = self.accounts[self.Customer_Id]['PhoneNo']
            w5 = self.accounts[self.Customer_Id][self.AcctNo]['accountNumber']
            w6 = self.accounts[self.Customer_Id][self.AcctNo]['AccountBalance']
            print('Bank ID:%s\nBank Name: %s\nBank Location: %s\n' % (self.Bank_Id, self.Bankname, self.Location))
            print('Customer_Id: %s\nCustomer_Name: %s\nAddress: %s\nPhoneNo.: %s \n' % (w1, w2, w3, w4))
            print('AccountNo: %s\nAccountBalance: %s\n' % (w5, w6))
            try:
                x = self.accounts[self.Customer_Id]['loan']['loanbalance']
                y = self.accounts[self.Customer_Id]['loan']['loanType']
                print('Active_Loan: %s\n' % x)
                print('loan Type: %s\n' % y)
            except:
                print('Loan not activated for this Account')
        except:
            print('Account does not exist!')

    def DepositCash(self, Amount):
        self.Amount = Amount
        if self.Amount > 0:
            self.accounts[self.CustomerId][self.AcctNo]['AccountBalance'] += self.Amount

    def WithdrawCash(self, amount):
        self.amount = amount
        if 0 < self.amount < self.accounts[self.CustomerId][self.AcctNo]['AccountBalance']:
            self.accounts[self.CustomerId][self.AcctNo]['AccountBalance'] -= self.amount
        else:
            print('Insufficient balance')

    def OpenAccount(self):
        self.accounts[self.Customer_Id] = {}
        self.accounts[self.Customer_Id]['Name'] = self.Name
        self.accounts[self.Customer_Id]['CustomerId'] = self.CustomerId
        self.accounts[self.Customer_Id]['Address'] = self.Address
        self.accounts[self.Customer_Id]['PhoneNo'] = self.PhoneNo
        self.accounts[self.Customer_Id][self.AcctNo] = {}
        self.accounts[self.Customer_Id][self.AcctNo]['accountNumber'] = self.AcctNo
        self.accounts[self.Customer_Id][self.AcctNo]['AccountBalance'] = 0
        return self.accounts

    def CloseAccount(self):
        del self.accounts[self.Customer_Id]

    def AccessLoan(self, loanAmount):
        self.loanAmount = loanAmount
        try:
            self.accounts[self.Customer_Id][self.AcctNo]['accountNumber'] = self.AcctNo
        except:
            print('Your are not eligible for a loan')
        if self.loanAmount > (1.5 * (self.accounts[self.Customer_Id][self.AcctNo]['AccountBalance'])):
            print('Your not eligible')
        else:
            print('Request Successful')

    def AccessCard(self):
        try:
            self.accounts[self.Customer_Id][self.AcctNo]['accountNumber'] = self.AcctNo
        except:
            print('Your are not eligible for Card please create an account first!')


class Teller(CustomerMenu, Bank):
    def __init__(self,TellerName, Teller_Id, BankId, Bankname, Location, Customer_Id, AccountNo, Name, Address, PhoneNo):
        super(Teller, self).__init__(Bank_Id, Bankname, Location, Customer_Id, AccountNo, Name, Address, PhoneNo)
        self.TellerName = TellerName
        self.TellerId = Teller_Id

    def CollectMoney(self):
        if self.Amount > 0:
            self.accounts[self.Customer_Id][self.AcctNo]['AccountBalance'] += self.Amount
        else:
            print('INPUT AMOUNT GREATER THAN ZERO')

    def LoanAccess(self, loan_Id ,Type):
        self.loanType = Type
        self.loanId = loanId
        try:
            self.accounts[self.Customer_Id][self.AcctNo]['accountNumber'] = self.AcctNo
        except:
            print('Your are not eligible for a loan')
        if self.loanAmount > (1.5*(self.accounts[self.Customer_Id][self.AcctNo]['AccountBalance'])):
            print('Your not eligible')
        else:
            self.accounts[self.Customer_Id]['loan'] = {}
            self.accounts[self.Customer_Id]['loan']['loan_Id'] = self.loan_Id
            self.accounts[self.Customer_Id]['loan']['loanType'] = self.loanType
            self.accounts[self.Customer_Id]['loan']['loanbalance'] = -self.loanAmount
            print('loan account has been created!')

    def ForInfo(self):
        print('Bank ID:%s\nBank Name: %s\nBank Location: %s\n' % (self.Bank_Id, self.Bankname, self.Location))
        print('Teller Id: %s\nTeller Name: %s\n' % (self.Teller_Id, self.TellerName))

    def IssueCard(self):
        if self.accounts[self.Customer_Id][self.AcctNo]['accountNumber'] == self.AcctNo:
            print('Your request  for card was received and your Card is ready')
        else:
            print('Not eligible for card issuing')


class Account(CustomerMenu):
    pass


class Loan(CustomerMenu):
    def __init__(self, LoanId, Type, Account_Id, BankId, Bankname, Location, Customer_Id, AccountNo, Name, Address, PhoneNo):
        super(Loan, self).__init__(Bank_Id, Bankname, Location, Customer_Id, AccountNo, Name, Address, PhoneNo)
        self.LoanId = LoanId
        self.Type = Type
        self.AcctNo = AccountId


First_Bank = Bank(1, 'ORIENT BANK', 'MAKERERE')
Second_Bank = Bank(2, 'EQUITY BANK', 'MAKERERE')
v1 = int(input('Enter the Id of the Bank:\n'))
v2 = input('Enter the Bank Name: \n')
v3 = input('Enter the bank location:\n')
v4 = input('if your a customer enter A or if a teller enter B:\n')
if v4 == 'A':
    i = 1
    while i < 11:
        i += 1
        C1, C2, C3, C4 = input('Enter Customer Name:\n'), input('Enter your Address:\n'), \
                     int(input('Enter your phone Number:\n')), input('Enter Your Account Number:\n')
        Cus_1 = Customer(v1, v2, v3, i, C1, C2, C3, C4)
        while True:
            L = int(input('Enter: 1 for General inquiry , 2 for Depositing , 3 for withdrawing, 4 for Requesting,'
                          ' 5 for Loan Application, 6 Open Account, 7 Close Account, 8 Quit'))
            if L == 1:
                Cus_1.GeneralInquiry()
            elif L == 2:
                K = int(input('Please enter the amount you want to deposit in figure\n'))
                Cus_1.DepositMoney(F)
            elif L == 3:
                M = int('Please enter the amount you want to withdraw\n')
                Cus_1.WithdawMoney(G)
            elif L == 4:
                Cus_1.RequestCard()
            elif L == 5:
                N = input('Enter the amount of loan you need in figures\n')
                Cus_1.ApplyForLoan(H)
            elif L == 6:
                Cus_1.OpenAccount()
            elif L == 7:
                Cus_1.CloseAccount()
            elif L == 8:
                break
elif V4 == 'B':
    T11, T12, T13, v4, T21, T22, T23, = input('Teller Name:\n'), input('TellerID:\n'), input('Enter Customer Name:\n'),\
                          input('Enter your Address:\n'), int(input('Enter your phone Number')),\
                        input('Enter Your Account Number:\n'), input('Enter CustomerId:')
    Teller = Teller(T11, T12, v1, v2, v3, T23, T22, T13, v4, T21)

    while True:
        while True:
            p = int(input('Enter: 1 for General inquiry\n , 2 for Depositing\n , 3 for withdrawing\n, 4 for Requesting\n,'
                          ' 5 for Loan Application\n, 6 Open Account\n, 7 Close Account\n, 8 Quit\n, 9 Provide Info\n, '
                          '10  Work on loan Request\n, 11 IssueCard\n,'))
            if p == 1:
                Teller.GeneralInquiry()
            elif p == 2:
                K = int(input('Please enter the amount you want to deposit in figure\n'))
                Teller.DepositMoney(F)
            elif p == 3:
                M = int('Please enter the amount you want to withdraw\n')
                Teller.WithdrawMoney(G)
            elif p == 4:
                Teller.RequestCard()
            elif p == 5:
                N = input('Enter the amount of loan you need in figures\n')
                Teller.ApplyForLoan(H)
            elif p == 6:
                Teller.OpenAccount()
            elif p == 7:
                Teller.CloseAccount()
            elif p == 8:
                break
            elif p == 9:
                Teller.ProvideInfo()
            elif p == 10:
                y = int(input('Please Enter loanId for the  Customer:'))
                z = input('Enter loan type requested by Customer:')
                Teller.LoanRequest(y, z)
            elif p == 11:
                Teller.IssueCard()

