# twilio oa

1. Given two arrays of strings, one containing the prefixes (area code) and one with a long string of numbers (phone numbers), return the longest prefix corresponding to all phone numbers.

   

   **Input**: Area Code: ["213", "21358", "1234", "12"]
   Phone Numbers: ["21349049", "1204539492", "123490485904"]
   **Output**: ['213', '12', '1234']
   **Solution**: Use Trie to store all the prefix strings and then search for the phone numbers in the prefix tree (This solution passed all test cases)
   **Note**: Keep in mind that Phone Numbers array can be very long

   ```python
   class trie:
       def __init__(self):
           self.trie = {}
       def construct(self, area_code):
           for code in area_code:
               t = self.trie
               for w in code:
                   t = t.setdefault(w, {})
               t['#'] = {}
       def find(self, number):
           t = self.trie
           res = ''
           for i, n in enumerate(number):
               if '#' in t:
                   res = number[:i]
               t = t.setdefault(n, {})
           return res
   def main():
       t = trie()
       area_code = ["1415123", "1415000", "1412", "1510", "1", "44"]
       phone_number = ["14151234567", "9990", "1415122983"]
       t.construct(area_code)
       res = []
       for number in phone_number:
           res.append(t.find(number))
       return res
   if __name__ == "__main__":
       r = main()
       print(r)
   ```

2. 