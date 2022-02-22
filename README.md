#### Attach_Request-Fuzzer

This modification to the srsue part in [srsRAN code](https://github.com/srsran/srsRAN) permits fuzzing on the NAS layer. More precisely it modifies the attach request sent by the UE to the MME in five methods (test cases):
 1. adding padding bytes between the UE network capability element and the ESM message container element
 2. appending padding bytes to the end of the attach request
 3. manipulating the length field of the UE network capability element
 4. inserting bytes into the UE network capability element with adjusting the length field
 5. adding additional UE security capabilities element in invalid ways

 To specify which method is to be used, pass ` --fuzz-case <number of the method> ` as an argument. 

 Moreover, to specify the number of bytes which are to be added, or to assign a new length to the length field in th UE network capability part, pass ` --modification <custom modification> ` as an argument.
 For test case 5 modification can have a value from 1 to 4 as follows:
 1. modification 1: adds a valid additional UE security capabilities element (for comparison)
 2. modification 2: adds a valid additional UE security capabilities element followed with one filled with zeros
 3. modification 3: adds an additional UE security capabilities element filled with zeros followed with a valid one 
 4. modification 4: adds an additional UE security capabilities element appended with a ox00 byte, exceeding by that the standard length for this element

## Examples:
* `srsue --fuzz-case 2 --modification 10` 

    will append 10 padding bytes to the end of the attach request

* `srsue --fuzz-case 3 --modification 9`

    will change the length field in the UE network capability part to 9
