# Item 25: Use async Functions Instead of Callbacks for Asynchronous Code

- callback < promise < async/await
- async declare > Promise<any>

• Prefer Promises to callbacks for better composability and type flow.
• Prefer async and await to raw Promises when possible. They produce more con‐ cise, straightforward code and eliminate whole classes of errors.
• If a function returns a Promise, declare it async.
