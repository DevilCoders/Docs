This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Project tasks implementation workflow

Any new task should be represented by a branch began from the 'trunk' branch:

```bash
arc checkout -b <new-branch-name> trunk
```

Once the work is finished the time to make a commit comes:

```bash
arc commit -m <commit-message-string>
```

## Some local scripts overview

1. Run the development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result. The page auto-updates as you edit the files.

2. Build the project:

```bash
npm run build
```

3. Code check with the prettier:

```
npm run prettier-check
```

4. Fix code error found by the prettier:

```
npm run prettier-fix
```

This command is meant to modify an existing code to bring it to compliance with the rules regarding the formatting and syntax. These rules are described in the .eslintrc file in the root project's directory.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.
