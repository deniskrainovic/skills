# Sketch forms

Forms for the expectation sketch in step 2. Pick the smallest one that makes the claim's "should" clear; one form per claim is usual, two is the most. Keep only the calls, files, states and boundaries the claim depends on.

Every sketch lands in the index inside a `<pre>`, so it must read as plain text. No Mermaid or other script-rendered diagrams: the index opens from disk without a network.

- Logic or an algorithm as pseudocode:

```text
on(save)
  if content is unchanged
    return cached result
  write new content
  return fresh result
```

- Runtime control flow as a call tree:

```text
submitForm
  createSession
    persistPrompt
    launchAgent
  navigateToSession
```

- Interaction between actors as a sequence, one arrow per message:

```text
User    -> UI      : choose command
UI      -> Daemon  : send expanded prompt
Daemon --> UI      : stream result
UI      -> User    : show result card
```

- UI structure as a component tree, with the state and module boundaries that matter:

```tsx
<SessionPage> (apps/example/src/routes/session.tsx)
  useSessionEvents()
  <SessionToolbar>
    <RunSkillButton> (packages/ui)
```

- File responsibility as a shallow file tree:

```text
src/
├── commands/       # parses user actions
├── sessions/       # owns session state
└── transport/      # sends API requests
```

- A state flow as transitions, including the ones that must be refused:

```text
draft     --submit-->   pending
pending   --approve-->  published
pending   --reject-->   draft
published --submit-->   (refused, stays published)
```

- A before/after as a `diff`, when the point is what changes and the surrounding shape already exists. Match the diff shape to the claim:

```diff
 on(save)
-  write content
+  if content is unchanged
+    return cached result
+  write new content
+  invalidate cache
```

```diff
 submitForm
   createSession
     persistPrompt
+    expandSkillMention
     launchAgent
```

```diff
 GET /admin/x as Reader
-  200, page rendered
+  403, body without the permission name
```

In the index, wrap added lines in `<ins>` or colour them green and removed lines red, so the diff still reads without syntax highlighting.

- Two dimensions (role times page, input times state) are not a sketch but a matrix; see step 1.

- A visual expectation (layout, a UI state comparison) that plain text cannot carry: a small inline SVG in the index, or a reference screenshot of the intended state marked as "expected", placed beside the observed one.
