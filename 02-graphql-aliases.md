


### Aliases

1. Try executing this query:

        {
        	organization(login: "facebook") {
            login
            members {
              totalCount
            }
          }
        	organization(login: "Netflix") {
            login
            members {
              totalCount
            }
          }
        }


    What happens? And what does the error actually mean?

2. _Aliases_ offer a way around this problem. An alias simply
   lets you choose an alternate name for a returned subtree.

   1. To create an alias, put your new name and a ':' before
      a field, like this:

          {
            a: organization(login: "facebook") {
              login
              members {
                totalCount
              }
            }
            b: organization(login: "Netflix") {
              login
              members {
                totalCount
              }
            }
          }


      Now the two subtrees are disambiguated.

   2. Try adding an alias for another field too. In this way, you have some control in shaping the response to your needs.
