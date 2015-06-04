# Hello World

| a | test |
| of some of the possibilities | hello again |

Some Code:

``` cpp
    // Print difference list in human readable format
    static void s_PrintDiff(const string& msg, const string& s1, const string& s2,
        const CDiffList& diff)
    {
        NcbiCout << msg << NcbiEndl
            << "Comparing '" << s1 << "' to '" << s2 << "':" << NcbiEndl;
        ITERATE(CDiffList::TList, it, diff.GetList()) {
            string op;
            size_t n1 = 0;
            size_t n2 = 0;

            if (it->IsDelete()) {
                op = "-";
                n1 = it->GetLine().first;
            } else if (it->IsInsert()) {
                op = "+";
                n2 = it->GetLine().second;
            } else {
                op = "=";
                n1 = it->GetLine().first;
                n2 = it->GetLine().second;
            }
            NCbiCout << op << " ("
                 << n1 << "," << n2 << ")"
                 << ": " << "'" << it->GetString() << "'" << NCbiEndl;
        }
    }

    // Perform a character-based diff:
    {{
        CTempString s1("how now");
        CTempString s2("brown cow");
        CDiff d;
        CDiffList& diffs(d.Diff(s1, s2));
        s_PrintDiff("Line-based diff:", s1, s2, diffs);
    }}

    // Perform a line-based diff:
    {% raw %}{{
        CTempString s1("group 1\nasdf asf\ntttt\nasdf asd");
        CTempString s2("group 2\nqwerty\n\nasdf\nasf asd");
        CDiffText d;
        CDiffList& diffs(d.Diff(s1, s2));
        s_PrintDiff("Line-based diff:", s1, s2, diffs);
    }}{% endraw %}
```
