# Housing Randomizer
Housing Randomizer for a field experiment on discrimination in the rental housing market. I have created the program in LiveCode, adopted to cater for three languages (German, French, Italian).

## Files
There is the LiveCode stack, and separately the code of the "generate" button, which does the randomization. I have put the code for the "generate" button for those who are interested in the workings of the program without wanting to install LiveCode.

## LiveCode Stack
The LiveCode stack was tested in versions 8 and 9 of LiveCode, and the assistants used compiled versions for Windows and Mac.

The LiveCode stack consists of several cards, which contain various data. For normal usage, we only need to use the first card ["Home"]. There are some settings on the first card, like the user name (=assistant name). Two probablities can be set here, but typically we would not change them on a day-to-day basis: the probabilitiy that a message includes a doctor title, and the probability of sending the default message.

We have designed the program/templates to work with properties with 1 to 6 rooms, and only included residential properties (no garages etc.), and only for apartments/flats (not houses). We recorded the URL of the property advert in the spreadsheet we used alongside to record everything, including the responses. We included a few variables on the landlord in the spreadsheet directly (e.g. private landlord), as well as the ZIP code.

The LiveCode stack works in three languages, even though the user interface is always in English. We chose to send messages in the language of the advert. To generate the messages, we need the number of rooms advertised, the location (municipality, city), the object name (as advertised), the rent. We also record the neighbourhood rent where this is mentioned in the adverts, though this is not relevant for the messages generated.

From a user's perspective, the next step is to click on the "generate" button, and then click on the "copy spreadsheet" button. The first will generate the profiles of the applicants, and the messages to be sent. The second will copy this information ready to be pasted into a spreadsheet. *Note, there is an omission in the code (a bug if you prefer), that we do not record the age of the applicant in the spreadsheet.* The code of the "copy spreadsheet" button works OK with Google sheets on Chrome and Firefox on most platforms, though sometimes "paste special" (Ctr+Shift+V) is needed for it to work rather than pasting with Ctrl+V. We had most success with the following combinations: Chrome on Windows; Chrome or Safari on Mac; Firefox and Chrome on GNU/Linux.

Where the contact form asks for additional information, we add this information from the profiles created, and record this in the spreadsheet by putting 1 in the corresponding "Used?" column. The randomizer always generates all the details, even though most of this information is never revealed to the landlords. *Note, there is an omission in the code (a bug if you prefer), that we do include a "Used?" field for income, so we did not record whether the income was declared to the landlord. Very few forms asked for income at this stage of the application, and we always generate similar (but not identical) incomes for the two candidates that are 'realistic' in relation to the advertised rent.*

The second card ["Names"] contains a series of text field, in which the names of the applicants are stored. We use 12 given (6 male, 6 female) and 6 family names for each ethnic minority group (Kosovo, Turkey, Germany, Italy, France), and for each language region (German Swiss, French Swiss, Italian Swiss). These are randomly combined within the group. For the Turkish family names, we included a variant with and without accents. The e-mail addresses correspond to the family names. They are listed twice in the case of the Turkish names because the accented and non-accented family names use the same (non-accented) e-mail address.

The third card ["Details"] contains a list of "origins", and permit types for the foreigners. There lists of jobs. There is a list of 5 jobs requiring high skill levels, and 5 jobs requiring low skill levels, each in a male and female version, and in three languages. As with the names, these data are independent of the working of the randomizer.

The card ["Addresses"] contains 6 addresses, two each in each of the three language regions. We used two phone numbers, because we did not respond to non-written contacts.

The card ["Default messages"] contains the default messages to be sent when indicated. We have adapted a default message from Comparis.ch, but for the French version a female and a male variant were necessary.

There follow three cards with the ["Templates"], in German (DE), Italian (IT), and French (FR). We used 36 templates for each language. Each template exists for male and female applicants for linguistic reasons, although the two can be equivalent. We also have templates for single applicants, applicants living as coples, and for families (which children). There are two templates each in a neutral (T1, T2), a negative (T3, T4), and a positive (T5, T6) language. The contents of the text fields is LiveCode code that produces the messages on the basis of variables defined in the "generate" button. Some of the variables come in several forms to allow for natural sentences and natural flow. For this reasons, some of the templates include optional "ands" as variables, too.

### Known Bugs

There are two known bugs in the code, as described above. First, we do not record age as a separate column in the spreadsheet. This infomation can be extracted (using a simple regex) from the message sent. Second, we do not generate a "Used?" column for income. This means we are unable to record whether income was declared, though it is very rare to ask for the income at this stage of the application process, and in none of the applications was it asked without also asking for the name of the employer (which we did not generate, hence we skipped the property anyway). This is why we managed not to spot it for very long.
