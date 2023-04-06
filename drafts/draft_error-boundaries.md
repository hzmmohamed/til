I almost completely forgot to put error boundaries in the Compass UI.
I was more focused writing type-safe than catching all kinds of errors with an error boundary.
Perhaps generic error boundaries are not much of a good idea anyway, because using types right would force you to handle the "fallback" case anyway.
Do we need explict error boundaries?

ts-pattern pushes me anyway to handle all cases, I have to give the types that cover the error cases.
