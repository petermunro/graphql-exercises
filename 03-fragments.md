## Fragments

A fragments is a group of fields that can be reused.

1.  Execute this query:

        {
            first: organization(login: "facebook") {
                login
                id
                url
                membersWithRole {
                  totalCount
                }
            }
            second: organization(login: "Netflix") {
                id
                url
                membersWithRole {
                  totalCount
                }
            }
        }

    > Note: Auto-complete doesn't work when using aliases in GraphiQL (bug?). Remove the alias temporarily to see the correct autocompletions.

2.  This can be rewritten, as there is duplication across the subfields. First, define a fragment that contains the fields you want to reuse, but don't execute the query yet:


        fragment orgFields on Organization {
          login
          location
          websiteUrl
          membersWithRole {
            totalCount
          }
        }

> You can choose the fragment name (I've chosen `orgFields`).
> Fragments must specify the _type_ they apply to. This is
> what the `on` clause does, and enables the fragment fields to be
> type checked.

Now apply this fragment by using the _spread_ operator (`...`) before the fragment name. Type the following query either before or after your fragment definition, and execute it:

    {
      first: organization(login: "facebook") {
        login
        ...orgFields
      }
      second: organization(login: "Netflix") {
        ...orgFields
      }
    }

3. Now your turn. Retrieve the `User`s with `login`s "stubailo" and "gaearon", and
   the fields `login`,`name`,`createdAt`, `company`, `location` and `email`.
   Use fragments to reuse the common fields.

4. Notice that you can mix fields and fragments as we did in the `first` query above (`...orgFields` and `country`). What happens if you specify a field twice - in both the fragment and the query that uses it?

5. Can fragments contain nested fields?
