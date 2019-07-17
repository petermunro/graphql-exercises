# Adding a Mutation on the Server

### Aim: To Change the Brightness Level on a Light

Steps:

1. Update the schema to add a `setBrightness` mutation, taking an `ID` and an `Int`.

2. Create a `setBrightness` function which finds the `Light` with that `ID`
  and sets its `brightnessLevel` to the incoming parameter.

3. Your function should return the updated `Light`.

4. Test this in GraphiQL.


