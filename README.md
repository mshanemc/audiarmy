# #TheAudiArmy App is for tracking A Race Team's Cars, Drivers, and Sponsors

## Determine your Data Model

- You can Go to Set Up - Schema Builder to view your current out of the box Data Model
- It is important to put some thought into this, maybe even before you begin creating your app, in order to stick with Salesforce Best Practices
- Always try and remember to reutilize as much of what Salesforce gives you as possible where it makes sense. Salesforce provides many options here including:
  - Utilize Standard Objects and Fields as much as you can.
  - ReLabel the Standard Objects as needed; ie Opportunities to Teams
  - Create Custom Objects to house various data points where the above really doesn't make sense
  - Create Record Types for on Standard or Custom Objects as needed

## Extend your Data Model (Custom Objects and Record Types)

- As per the above options, I am choosing to do the following:
  - Create Record Types for Leads
    1. GoTo Object Manager, Search for and Click on Lead Object, Click on Record Type on the left, Create Lead Process - TheAudiArmy Leads
    2. Create Lead Record Type of Sponsor, choose Lead (Sales) Layout - later ReName to TheAudiArmy Sponsor Layout and then Clone Layout and ReNAme it TheAudiArmy Driver Layout
    3. Create Lead Record Type of Driver, choose TheAudiArmy Driver Layout
  - Create Record Types for Accounts
    1. Create Account Record Type of Sponsor, choose Account (Sales) Layout - later ReName to TheAudiArmy Sponsor Layout and then Clone Layout and ReNAme it TheAudiArmy Team Layout
    2. Create Account Record Type of Team, choose TheAudiArmy Team Layout
  - Create Record Types for Contacts
    1. Create Contact Record Type of Sponsor, choose Contact (Sales) Layout - later ReName to TheAudiArmy Sponsor Layout and then Clone Layout and ReNAme it TheAudiArmy Driver Layout
    2. Create Contact Record Type of Driver, choose TheAudiArmy Driver Layout
  - ReLabel Opportunity Object to Sponsorships
    1. Change Opportunity Owner to Sponsor Acquisition Owner/s
    2. Change Expected Revenue to Expected Sponsorship Amount
    3. Accept the rest of the standard suggested changes
  - Create Custom Object for Vehicles w/ 2 Record Types
    1. Record Name = Name
    2. Data Type = Text
    3. Click True for all of the Checkboxes when Creating the Custom Object
    4. Select the Keys Icon for the Tab
    5. Create Record Type of Car, TheAudiArmy Car Layout and then Clone Layout and ReNAme it TheAudiArmy Car Part Layout
    6. Create Record Type of Car Part, choose TheAudiArmy Car Part Layout
  - Create Custom Object for Hooning w/ 4 Record Types(Don’t use Activities so that you can utilize them properly later)
    1. Record Name = Hooning At
    2. Data Type = Text
    3. Click True for all of the Checkboxes when Creating the Custom Object
    4. Select the Icon for the Tab
    5. Create Record Type of Show, choose TheAudiArmy Show Layout and then Clone Layout and ReName it TheAudiArmy Race Layout, repeat for TheAudiArmy Road Course Layout, and then repeat for TheAudiArmy Drag Strip Layout
    6. Create Record Type of Race, choose TheAudiArmy Race Layout
    7. Create Record Type of Road Course, choose Road Course Layout
    8. Create Record Type of Drag Strip, choose TheAudiArmy Drag Strip Layout

## 3. Integrating Data Model through LookUp Fields connecting our Objects as Ohana

- Map Leads to Accounts / Contacts(no Opportunity)
- Relational Fields for the Vehicle and Hooning Custom Objects
  1. Vehicle Car Records need a LookUp field to look up to Contact Driver Records, placed on TheAudiArmy Car Layout and the Related List goes on TheAudiArmy Driver Layout
  2. Vehicles Car Part Records need a LookUp field to look up to Vehicle Car Records, placed on TheAudiArmy Car Part Layout and the Related List goes on TheAudiArmy Car Layout
  3. Hooning Show and Race Records need a LookUp field to look up to Contact Driver Records, placed on TheAudiArmy Show Layout and the Related List goes on TheAudiArmy Driver Layout
  4. ReUse Field above for the Hooning Show Records
  5. Hooning Drag Strip and Road Course Records need a LookUp field to look up to Hooning Race Records, placed on TheAudiArmy Drag Strip and Road Course Layout and the Related List goes on TheAudiArmy Race Layout
  6. ReUse Field above for the Hooning Road Course Records

## Configure Objects in Data Model

- Remove unneeded fields from Lead, Account, Contact, and Sponsor Page Layouts
- Add fields to collect Data Points needed for reporting
  1. Vehicle
     - Car Layout
       1. Number - 4 - Year
       2. Picklist - Make
       3. Text - 69 - Model
       4. Text - 69 - BOTH Layouts - Color
     - Car Part Layout
       1. LookUp - Account - Car Part Layout - Sponsor and Team Layout - Brand
       2. Picklist - Part Type
       3. Checkbox - Sponsored Part
       4. Text Area Rich - 999 / 10 - Part Description - BOTH Layouts
  2. Hooning
     - Show
       1. Text - 255 - ALL Layouts - Location
       2. Currency - 7 / 2 - BOTH Show and Race Layout - Payout
       3. Date/Time - BOTH Show and Race Layouts - Event Date
     - Race
       1. Number - 2 - Place
     - Drag Strip
       1. Number - 2 / 2 - BOTH Drag Strip and Road Course Layout - Track Length
       2. Number - 4 - 3 Layouts Race, Drag Strip, and Road Course Layout - Laps
     - Road Course
       1. Picklist - Clockwise / Counter Clockwise - Direction
  3. Sponsor
     - Sponsor
       1. Checkbox - Currently a Sponsor
       2. Checkbox - Target Sponsor
  4. Account
     - Sponsor
       1. Checkbox - Currently a Sponsor
       2. Checkbox - Target Sponsor
  5. Contact
     - Sponsor
       1. Checkbox - Point Man
       2. ReArrange fields we want to keep

## Remove unneeded Page Layouts

- Create the wrapper for the App
  1. GoTo SetUp - Search for App - click on App Manager
  2. Click New Lightning App Button
  3. Enter Name, Description, and Upload Logo
  4. Desktop and Phone
  5. All Relevant Objects
  6. All Profiles
- Test your App utilizing Sample Records
- Decide if you want to further customize your App
  1. Lead Settings
  2. Lead - Account, Contact, Sponsor mapping
  3. Enable “Enable Conversions for Salesforce Mobile”
  4. Enable “Hide Opportunity Section of Convert Lead Window”
  5. Enable “Select "Don't create an opportunity" by Default in Convert Lead Window”
- Automate your App
  1. Depending on if Users can Create Sponsor Opportunities based on above when Lead is converted; create a Lightning Process Builder
     - GoTo SetUp, Search Process B and then click on Process Builder on the left,
  2. ReAlign the Lightning Object Layout and Tabs including utilizing Dynamic Components to only show Related List items as applicable
  3. eMail Alerts to Team Members when Parts are Sponsored, new new Hoonings are posted, etc
