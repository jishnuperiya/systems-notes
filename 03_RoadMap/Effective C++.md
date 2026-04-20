

| Item | Rule                                  | Core Idea                    | Mental Trigger          | Read? |
| ---- | ------------------------------------- | ---------------------------- | ----------------------- | ----- |
| 1    | View C++ as federation of languages   | C, OO, templates, STL differ | “Which C++ am I using?” |       |
| 2    | Prefer const, enum, inline to #define | Type safety                  | “Am I using macros?”    |       |
| 3    | Use const whenever possible           | Safer interfaces             | “Should this be const?” |       |
| 4    | Make sure objects are initialized     | Avoid UB                     | “Is this initialized?”  |       |


| Item | Rule                                           | Core Idea           | Mental Trigger              | Read? |
| ---- | ---------------------------------------------- | ------------------- | --------------------------- | ----- |
| 5    | Know what functions compiler generates         | Default ops exist   | “What did compiler create?” |       |
| 6    | Explicitly disallow unwanted functions         | `=delete`           | “Should copying exist?”     |       |
| 7    | Declare virtual destructor in polymorphic base | Proper cleanup      | “Used via base ptr?”        |       |
| 8    | Prevent exceptions leaving destructors         | Avoid terminate     | “Can dtor throw?”           |       |
| 9    | Never call virtuals in ctor/dtor               | Incomplete object   | “Virtual here?”             |       |
| 10   | operator= returns *this                        | Convention          | “Chainable?”                |       |
| 11   | Handle self-assignment                         | Safety              | “a = a?”                    |       |
| 12   | Copy all parts                                 | Complete copy       | “Missed member?”            |       |
| 13   | Use RAII                                       | Resource safety     | “Who owns this?”            |       |
| 14   | Think about copying behavior                   | Ownership semantics | “What happens on copy?”     |       |
| 15   | Provide access to raw resources                | Controlled exposure | “Need raw pointer?”         |       |
| 16   | Match new/delete forms                         | UB otherwise        | “new[] or new?”             |       |
| 17   | Store new in smart pointer immediately         | Exception safety    | “Raw pointer escaping?”     |       |

| Item | Rule                                       | Core Idea             | Mental Trigger          | Read? |
| ---- | ------------------------------------------ | --------------------- | ----------------------- | ----- |
| 18   | Make interfaces easy to use correctly      | API design            | “Can user misuse this?” |       |
| 19   | Treat class design like type design        | Types define behavior | “What invariants?”      |       |
| 20   | Prefer pass-by-const-ref                   | Avoid copies          | “Expensive copy?”       |       |
| 21   | Don’t return handles to internals          | Encapsulation         | “Leaking internals?”    |       |
| 22   | Declare data members private               | Maintain invariants   | “Why is this public?”   |       |
| 23   | Prefer non-member non-friend               | Decoupling            | “Can this be free fn?”  |       |
| 24   | Declare non-member when conversions needed | Symmetry              | “Operator symmetry?”    |       |
| 25   | Consider swap support                      | Efficiency            | “Need fast swap?”       |       |

| Item | Rule                                 | Core Idea     | Mental Trigger           | Read? |
| ---- | ------------------------------------ | ------------- | ------------------------ | ----- |
| 26   | Delay variable definitions           | Efficiency    | “Can I delay this?”      |       |
| 27   | Minimize casting                     | Type safety   | “Why casting?”           |       |
| 28   | Avoid returning handles to internals | Safety        | “Dangling risk?”         |       |
| 29   | Strive for exception-safe code       | Guarantees    | “What if throw?”         |       |
| 30   | Understand inlining                  | Tradeoffs     | “Inline worth it?”       |       |
| 31   | Minimize compilation dependencies    | Faster builds | “Can I forward declare?” |       |

| Item | Rule                                                  | Core Idea            | Mental Trigger               | Read? |
| ---- | ----------------------------------------------------- | -------------------- | ---------------------------- | ----- |
| 32   | Public inheritance = is-a                             | Correct modeling     | “Is it really is-a?”         |       |
| 33   | Avoid hiding inherited names                          | Name hiding issue    | “Using base funcs?”          |       |
| 34   | Differentiate interface vs implementation inheritance | Virtual vs non       | “Override intent?”           |       |
| 35   | Consider alternatives to virtual                      | Templates, strategy  | “Need runtime polymorphism?” |       |
| 36   | Never redefine inherited non-virtual                  | Undefined behavior   | “Overriding non-virtual?”    |       |
| 37   | Never redefine default params                         | Static binding       | “Default args mismatch?”     |       |
| 38   | Model has-a with composition                          | Prefer composition   | “Better than inheritance?”   |       |
| 39   | Use private inheritance carefully                     | Implementation reuse | “Why not composition?”       |       |
| 40   | Use multiple inheritance judiciously                  | Complexity           | “Really need MI?”            |       |

| Item | Rule                                         | Core Idea                 | Mental Trigger              | Read? |
| ---- | -------------------------------------------- | ------------------------- | --------------------------- | ----- |
| 41   | Understand implicit interfaces               | Templates/contracts       | “What is required?”         |       |
| 42   | Use typename properly                        | Dependent names           | “Template parsing issue?”   |       |
| 43   | Access names in base templates               | Name lookup               | “Why not found?”            |       |
| 44   | Factor parameter-independent code            | Reduce bloat              | “Duplicate template code?”  |       |
| 45   | Use member templates for conversions         | Flexibility               | “Cross-type ops?”           |       |
| 46   | Define non-member inside templates carefully | ADL                       | “Where to place?”           |       |
| 47   | Use traits classes                           | Type info at compile time | “Need type property?”       |       |
| 48   | Use TMP for compile-time logic               | Meta programming          | “Can this be compile-time?” |       |

| Item | Rule                                        | Core Idea          | Mental Trigger              | Read? |
| ---- | ------------------------------------------- | ------------------ | --------------------------- | ----- |
| 49   | Understand type deduction                   | Templates behavior | “What type deduced?”        |       |
| 50   | Understand implicit conversions             | Template matching  | “Why overload chosen?”      |       |
| 51   | Control implicit conversions                | Explicit control   | “Too many conversions?”     |       |
| 52   | Use overloading vs specialization carefully | Resolution rules   | “Which wins?”               |       |
| 53   | Be aware of template bloat                  | Code size          | “Too many instantiations?”  |       |
| 54   | Use placement new carefully                 | Manual control     | “Managing memory manually?” |       |
