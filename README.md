from PIL import Image
from pyocr import pyocr
from pyocr import builders
import re, datetime
import sys
import pyocr
import pyocr.builders
import pytesseract
from invoice2data import extract_data
import datefinder
import parsedatetime
from dateutil.parser import parse
from dateparser.search import search_dates

pyocr.tesseract.TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"

tools = pyocr.get_available_tools()
if len(tools) == 0:
    print("No OCR tool found")
    sys.exit(1)
# The tools are returned in the recommended order of usage
tool = tools[0]

langs = tool.get_available_languages()
lang = langs[0]
print("Will use lang '%s'" % (lang))
image = "G:\\chandan\\Aadhar card& SBI\\All Semester " \
        "Marksheet\\All-semester-scanned\\Receipts\\x5.jpeg"
# image = "http://www.domain.com/fr/i/3518721/phone"(give path of the image)
text = tool.image_to_string(
    Image.open(image),
    builder=pyocr.builders.TextBuilder())
print(text)

dates = search_dates(text)
for each_dates in dates:

    matches = datefinder.find_dates(str(each_dates[0]))
    for match in matches:

        regex = re.findall(r"[\d]{1,2}/[\d]{1,2}/[\d]{4}", str(match))

        for s in regex:
            string_date = str(match)
            if '2019' in string_date:
                print(string_date[0:11])

        regex = re.findall(r"[\d]{1,2}-[\d]{1,2}-[\d]{2}", str(match))

        for s in regex:
            string_date = str(match)
            if '2019' in string_date:
                print(string_date[0:11])

        regex = re.findall(r"[\d]{1,2} [ADFJMNOS]\w* [\d]{4}", str(match))

        for s in regex:
            string_date = str(match)
            if '2019' in string_date:
                print(string_date[0:11])

        regex = re.findall(r"[\d]{1,2} [ADFJMNOS]\w* [\d]{4}", str(match))

        for s in regex:
            string_date = str(match)
            if '2019' in string_date:
                print(string_date[0:11])
