### Haskell Exercises Solutions

#### Beginner (1-25)

1. **Factorial Calculation:**
   Implement a function to calculate the factorial of a number.
   ```haskell
   factorial :: Integer -> Integer
   factorial 0 = 1
   factorial n = n * factorial (n - 1)
   ```

2. **Fibonacci Sequence:**
   Write a function to generate the nth Fibonacci number.
   ```haskell
   fibonacci :: Integer -> Integer
   fibonacci 0 = 0
   fibonacci 1 = 1
   fibonacci n = fibonacci (n - 1) + fibonacci (n - 2)
   ```

3. **Palindrome Checker:**
   Create a function to check if a given string is a palindrome.
   ```haskell
   isPalindrome :: String -> Bool
   isPalindrome str = str == reverse str
   ```

4. **Sum of Squares:**
   Implement a function to compute the sum of squares of a list of integers.
   ```haskell
   sumOfSquares :: [Integer] -> Integer
   sumOfSquares xs = sum [x^2 | x <- xs]
   ```

5. **List Reversal:**
   Write a function to reverse a list without using built-in functions.
   ```haskell
   reverseList :: [a] -> [a]
   reverseList [] = []
   reverseList (x:xs) = reverseList xs ++ [x]
   ```

6. **Filter Even Numbers:**
   Implement a function to filter out even numbers from a list.
   ```haskell
   filterEven :: [Integer] -> [Integer]
   filterEven xs = filter even xs
   ```

7. **Merge Sort:**
   Create an implementation of the merge sort algorithm.
   ```haskell
   mergeSort :: Ord a => [a] -> [a]
   mergeSort [] = []
   mergeSort [x] = [x]
   mergeSort xs = merge (mergeSort left) (mergeSort right)
     where
       (left, right) = splitAt (length xs `div` 2) xs
       merge [] ys = ys
       merge xs [] = xs
       merge (x:xs) (y:ys)
         | x <= y    = x : merge xs (y:ys)
         | otherwise = y : merge (x:xs) ys
   ```

8. **Matrix Multiplication:**
   Implement matrix multiplication for 2x2 matrices.
   ```haskell
   type Matrix = [[Integer]]

   matrixMultiply :: Matrix -> Matrix -> Matrix
   matrixMultiply a b = [[sum $ zipWith (*) ar bc | bc <- transpose b] | ar <- a]
     where
       transpose ([]:_) = []
       transpose xs = (map head xs) : transpose (map tail xs)
   ```

9. **Implement `Maybe` Monad:**
   Define a simple version of the `Maybe` monad and implement basic operations.
   ```haskell
   data Maybe a = Nothing | Just a

   instance Functor Maybe where
     fmap _ Nothing  = Nothing
     fmap f (Just x) = Just (f x)

   instance Applicative Maybe where
     pure = Just
     Nothing <*> _ = Nothing
     (Just f) <*> something = fmap f something

   instance Monad Maybe where
     return = Just
     Nothing >>= _ = Nothing
     (Just x) >>= f = f x
   ```

10. **File I/O:**
    Write a function to count the number of lines in a file.
    ```haskell
    countLines :: FilePath -> IO Int
    countLines filePath = do
      content <- readFile filePath
      return $ length (lines content)
    ```

11. **Parse a CSV File:**
    Implement a function to parse a CSV file into a list of lists of strings.
    ```haskell
    import Data.List.Split (splitOn)

    parseCSV :: String -> [[String]]
    parseCSV = map (splitOn ",") . lines
    ```

12. **Generate Primes:**
    Write a function to generate all prime numbers up to a given number using the Sieve of Eratosthenes.
    ```haskell
    sieve :: [Integer] -> [Integer]
    sieve [] = []
    sieve (p:xs) = p : sieve [x | x <- xs, x `mod` p /= 0]

    primes :: Integer -> [Integer]
    primes n = sieve [2..n]
    ```

13. **Create a Binary Tree:**
    Implement a simple binary tree and provide functions for insertion and traversal.
    ```haskell
    data Tree a = Empty | Node a (Tree a) (Tree a) deriving (Show)

    insert :: Ord a => a -> Tree a -> Tree a
    insert x Empty = Node x Empty Empty
    insert x (Node y left right)
      | x < y     = Node y (insert x left) right
      | otherwise = Node y left (insert x right)

    inorder :: Tree a -> [a]
    inorder Empty = []
    inorder (Node x left right) = inorder left ++ [x] ++ inorder right
    ```

14. **Convert to Roman Numerals:**
    Implement a function that converts an integer to a Roman numeral.
    ```haskell
    intToRoman :: Int -> String
    intToRoman n = concat $ map (\(v, r) -> replicate (n `div` v) r) values
      where
        values = [(1000, "M"), (900, "CM"), (500, "D"), (400, "CD"), (100, "C"),
                  (90, "XC"), (50, "L"), (40, "XL"), (10, "X"), (9, "IX"),
                  (5, "V"), (4, "IV"), (1, "I")]
    ```

15. **Concurrent Programming:**
    Write a program using `forkIO` to print "Hello" and "World" concurrently.
    ```haskell
    import Control.Concurrent

    main :: IO ()
    main = do
      forkIO $ putStrLn "Hello"
      forkIO $ putStrLn "World"
      threadDelay 1000000  -- Wait a bit for threads to finish
    ```

16. **Custom List Monad:**
    Create a custom monad based on lists and demonstrate its use.
    ```haskell
    newtype ListMonad a = ListMonad { getList :: [a] }

    instance Functor ListMonad where
      fmap f (ListMonad xs) = ListMonad (map f xs)

    instance Applicative ListMonad where
      pure x = ListMonad [x]
      (ListMonad fs) <*> (ListMonad xs) = ListMonad [f x | f <- fs, x <- xs]

    instance Monad ListMonad where
      return = pure
      (ListMonad xs) >>= f = ListMonad (concatMap (getList . f) xs)
    ```

17. **Implement `Applicative`:**
    Implement the `Applicative` type class for a simple custom type.
    ```haskell
    data Box a = Box a

    instance Functor Box where
      fmap f (Box x) = Box (f x)

    instance Applicative Box where
      pure = Box
      (Box f) <*> (Box x) = Box (f x)
    ```

18. **Parse JSON Data:**
    Use a JSON library to parse JSON data and extract specific fields.
    ```haskell
    import Data.Aeson
    import qualified Data.ByteString.Lazy as B

    data User = User { name :: String, age :: Int } deriving Show

    instance FromJSON User where
      parseJSON = withObject "User" $ \v -> User
        <$> v .: "name"
        <*> v .: "age"

    parseUser :: FilePath -> IO (Maybe User)
    parseUser filePath = do
      jsonData <- B.readFile filePath
      return $ decode jsonData
    ```

19. **Software Transactional Memory:**
    Implement a counter using STM (Software Transactional Memory) for safe concurrent updates.
    ```haskell
    import Control.Concurrent.STM

    main :: IO ()
    main = do
      counter <- newTVarIO (0 :: Int)
      atomically $ modifyTVar' counter (+1)
      value <- readTVarIO counter
      print value
    ```

20. **Property-Based Testing:**
    Write property-based tests for a function using the `QuickCheck` library.
    ```haskell
    import Test.QuickCheck

    prop_reverse :: [Int] -> Bool
    prop_reverse xs = (reverse . reverse) xs == xs

    main :: IO ()
    main = quickCheck prop_reverse
    ```

21. **Count Vowels:**
    Create a function that counts the number of vowels in a string.
    ```haskell
    countVowels :: String -> Int
    countVowels str = length [c | c <- str, c `elem` "aeiouAEIOU"]
    ```

22. **Find Maximum:**
    Write a function to find the maximum value in a list.
    ```haskell
    findMax :: (Ord a) => [a] -> a
    findMax [] = error "Empty list"
    findMax (x:xs) = foldl1 max (x:xs)

    ```

23. **Generate Combinations:**
    Implement a function to generate all combinations of a list.
    ```haskell
    combinations :: [a] -> [[a]]
    combinations [] = [[]]
    combinations (x:xs) = ys ++ map (x:) ys
      where ys = combinations xs
    ```

24. **Count Elements:**
    Create a function that counts occurrences of each element in a list.
    ```haskell
    countElements :: (Eq a) => [a] -> [(a, Int)]
    countElements xs = [(x, count x xs) | x <- unique xs]
      where
        unique = foldr (\x acc -> if x `elem` acc then acc else x : acc) []
        count x = length . filter (== x)
    ```

25. **Flatten a List:**
    Implement a function to flatten a list of lists.
    ```haskell
    flatten :: [[a]] -> [a]
    flatten = foldr (++) []
    ```

Here are the solutions to the intermediate Haskell exercises from 26 to 50, along with explanations and code.

### Haskell Exercises Solutions

#### Intermediate (26-50)

26. **Binary Search:**
   Implement a binary search algorithm.
   ```haskell
   binarySearch :: (Ord a) => a -> [a] -> Maybe Int
   binarySearch _ [] = Nothing
   binarySearch x xs = binarySearch' x xs 0 (length xs - 1)
     where
       binarySearch' _ [] _ _ = Nothing
       binarySearch' x xs low high
         | low > high = Nothing
         | midValue == x = Just mid
         | midValue < x = binarySearch' x xs (mid + 1) high
         | otherwise = binarySearch' x xs low (mid - 1)
         where
           mid = (low + high) `div` 2
           midValue = xs !! mid
   ```

27. **Balanced Parentheses:**
   Write a function to check if parentheses in a string are balanced.
   ```haskell
   balancedParentheses :: String -> Bool
   balancedParentheses str = checkBalance str 0
     where
       checkBalance [] 0 = True
       checkBalance [] _ = False
       checkBalance (x:xs) n
         | x == '('  = checkBalance xs (n + 1)
         | x == ')'  = n > 0 && checkBalance xs (n - 1)
         | otherwise = checkBalance xs n
   ```

28. **Unique Elements:**
   Implement a function to remove duplicate elements from a list.
   ```haskell
   uniqueElements :: (Eq a) => [a] -> [a]
   uniqueElements = foldr (\x acc -> if x `elem` acc then acc else x : acc) []
   ```

29. **Zip Lists:**
   Create a function to zip two lists into a list of tuples.
   ```haskell
   zipLists :: [a] -> [b] -> [(a, b)]
   zipLists [] _ = []
   zipLists _ [] = []
   zipLists (x:xs) (y:ys) = (x, y) : zipLists xs ys
   ```

30. **Longest Common Prefix:**
   Write a function that finds the longest common prefix in a list of strings.
   ```haskell
   longestCommonPrefix :: [String] -> String
   longestCommonPrefix [] = ""
   longestCommonPrefix xs = foldr commonPrefix (head xs) (tail xs)
     where
       commonPrefix s1 s2 = takeWhile (uncurry (==)) (zip s1 s2)
   ```

31. **Nth Largest Element:**
   Implement a function to find the nth largest element in a list.
   ```haskell
   nthLargest :: (Ord a) => Int -> [a] -> Maybe a
   nthLargest n xs
     | n <= 0 || n > length unique = Nothing
     | otherwise = Just (unique !! (n - 1))
     where
       unique = reverse . take (length xs) . removeDuplicates . sort $ xs
       removeDuplicates = foldr (\x acc -> if x `elem` acc then acc else x : acc) []
   ```

32. **Anagram Checker:**
   Write a function to check if two strings are anagrams.
   ```haskell
   areAnagrams :: String -> String -> Bool
   areAnagrams s1 s2 = sorted s1 == sorted s2
     where sorted = sort . filter (/= ' ')
   ```

33. **Group Anagrams:**
   Implement a function to group anagrams from a list of strings.
   ```haskell
   groupAnagrams :: [String] -> [[String]]
   groupAnagrams xs = Map.elems $ foldr group Map.empty xs
     where
       group x acc = Map.insertWith (++) (sort x) [x] acc
   ```

34. **Count Words:**
   Create a function to count the number of words in a string.
   ```haskell
   countWords :: String -> Int
   countWords str = length (words str)
   ```

35. **Flatten and Remove Duplicates:**
   Write a function to flatten a nested list and remove duplicates.
   ```haskell
   flattenAndRemoveDuplicates :: (Eq a) => [[a]] -> [a]
   flattenAndRemoveDuplicates xs = unique (concat xs)
     where
       unique [] = []
       unique (y:ys) = y : unique (filter (/= y) ys)
   ```

36. **Transpose a Matrix:**
   Implement a function to transpose a given matrix.
   ```haskell
   transposeMatrix :: [[a]] -> [[a]]
   transposeMatrix ([]:_) = []
   transposeMatrix xs = map head xs : transposeMatrix (map tail xs)
   ```

37. **Find the Mode:**
   Write a function to find the mode of a list.
   ```haskell
   findMode :: (Ord a) => [a] -> [a]
   findMode xs = maximumBy (compare `on` length) (group (sort xs))
   ```

38. **Implement `Functor`:**
   Define and implement the `Functor` type class for a custom type.
   ```haskell
   data Box a = Box a

   instance Functor Box where
     fmap f (Box x) = Box (f x)
   ```

39. **Basic HTTP Client:**
   Use a library to implement a simple HTTP client that fetches data from a URL.
   ```haskell
   import Network.HTTP.Simple

   fetchURL :: String -> IO ()
   fetchURL url = do
     response <- httpLBS url
     print $ getResponseBody response
   ```

40. **Simple Event Loop:**
   Create a simple event loop that processes events from a queue.
   ```haskell
   import Control.Concurrent
   import Control.Monad

   eventLoop :: MVar [String] -> IO ()
   eventLoop queue = forever $ do
     events <- takeMVar queue
     case events of
       [] -> return ()
       (event:rest) -> do
         putStrLn event
         putMVar queue rest
   ```

41. **Implement `Foldable`:**
   Implement the `Foldable` type class for a custom data type.
   ```haskell
   data MyList a = Empty | Cons a (MyList a)

   instance Foldable MyList where
     foldMap _ Empty = mempty
     foldMap f (Cons x xs) = f x `mappend` foldMap f xs
   ```

42. **Memoization:**
   Write a memoization function to optimize recursive computations.
   ```haskell
   import Data.Map.Strict (Map)
   import qualified Data.Map.Strict as Map

   memoize :: (Int -> a) -> Int -> a
   memoize f = (Map.!) table
     where
       table = Map.fromList [(n, f n) | n <- [0..]]
   ```

43. **Implement `Foldl` and `Foldr`:**
   Define your versions of `foldl` and `foldr`.
   ```haskell
   myFoldr :: (a -> b -> b) -> b -> [a] -> b
   myFoldr _ acc [] = acc
   myFoldr f acc (x:xs) = f x (myFoldr f acc xs)

   myFoldl :: (b -> a -> b) -> b -> [a] -> b
   myFoldl _ acc [] = acc
   myFoldl f acc (x:xs) = myFoldl f (f acc x) xs
   ```

44. **Create a State Monad:**
   Implement a simple state monad and demonstrate its use.
   ```haskell
   newtype State s a = State { runState :: s -> (a, s) }

   instance Functor (State s) where
     fmap f (State g) = State $ \s -> let (a, s') = g s in (f a, s')

   instance Applicative (State s) where
     pure x = State $ \s -> (x, s)
     State f <*> State g = State $ \s ->
       let (h, s1) = f s
           (a, s2) = g s1
       in (h a, s2)

   instance Monad (State s) where
     State g >>= f = State $ \s ->
       let (a, s') = g s
       in runState (f a) s'
   ```

45. **Count Characters:**
   Write a function that counts the occurrences of each character in a string.
   ```haskell
   import Data.Map.Strict (Map)
   import qualified Data.Map.Strict as Map

   countCharacters :: String -> Map Char Int
   countCharacters str = foldr (\c acc -> Map.insertWith (+) c 1 acc) Map.empty str
   ```

46. **Implement `Either`:**
   Create a simple version of the `Either` type and demonstrate its use.
   ```haskell
   data Either a b = Left a | Right b

   instance Functor (Either a) where
     fmap _ (Left x) = Left x
     fmap f (Right y) = Right (f y)

   instance Applicative (Either a) where
     pure = Right
     Left x <*> _ = Left x
     Right f

 <*> y = fmap f y

   instance Monad (Either a) where
     Left x >>= _ = Left x
     Right y >>= f = f y
   ```

47. **Text Justification:**
   Implement a function to justify text to a specific width.
   ```haskell
   justifyText :: Int -> String -> String
   justifyText width str = unwords (map justifyLine (lines str))
     where
       justifyLine line
         | length words' < 2 = line
         | otherwise = unwords $ addSpaces (words line)
         where
           words' = words line
           totalSpaces = width - sum (map length words')
           spacesNeeded = length words' - 1
           spaces = replicate spacesNeeded (totalSpaces `div` spacesNeeded)
           addSpaces [] = []
           addSpaces [x] = [x]
           addSpaces (x:xs) = x : (take spacesNeeded (cycle spaces)) ++ addSpaces xs
   ```

48. **Sort by Frequency:**
   Write a function to sort a list of elements by their frequency of occurrence.
   ```haskell
   import Data.List (group, sortOn)

   sortByFrequency :: (Ord a) => [a] -> [a]
   sortByFrequency xs = concat . sortOn (negate . length) . group . sort $ xs
   ```

49. **Rotate a List:**
   Implement a function that rotates a list by a given number of places.
   ```haskell
   rotate :: Int -> [a] -> [a]
   rotate n xs = take len . drop (n `mod` len) $ cycle xs
     where len = length xs
   ```

50. **Implement a Simple Calculator:**
   Create a basic calculator that evaluates simple arithmetic expressions.
   
   ```haskell
   import Text.Read (readMaybe)

   data Expr = Add Expr Expr | Sub Expr Expr | Num Int

   eval :: Expr -> Int
   eval (Num n) = n
   eval (Add x y) = eval x + eval y
   eval (Sub x y) = eval x - eval y

   parseExpr :: String -> Maybe Expr
   parseExpr str = parseTerm (words str)

   parseTerm :: [String] -> Maybe Expr
   parseTerm [x, "+", y] = Add <$> parseNum x <*> parseTerm [y]
   parseTerm [x, "-", y] = Sub <$> parseNum x <*> parseTerm [y]
   parseTerm [x] = parseNum x
   parseTerm _ = Nothing

   parseNum :: String -> Maybe Expr
   parseNum str = Num <$> readMaybe str
   ```

#### **Advanced (51-75)**

Here are solutions to the Haskell exercises from 51 to 75, along with explanations and code snippets.

### Haskell Exercises Solutions

#### Advanced (51-75)

51. **Quicksort Algorithm:**
   Implement the quicksort algorithm.
   ```haskell
   quicksort :: (Ord a) => [a] -> [a]
   quicksort [] = []
   quicksort (pivot:xs) =
     quicksort [x | x <- xs, x < pivot] ++ [pivot] ++ quicksort [x | x <- xs, x >= pivot]
   ```

52. **Implement `MonadPlus`:**
   Define and implement the `MonadPlus` type class.
   ```haskell
   import Control.Monad

   newtype Maybe' a = Just' a | Nothing' deriving (Show, Eq)

   instance Functor Maybe' where
     fmap f (Just' x) = Just' (f x)
     fmap _ Nothing' = Nothing'

   instance Applicative Maybe' where
     pure = Just'
     (Just' f) <*> (Just' x) = Just' (f x)
     _ <*> _ = Nothing'

   instance Monad Maybe' where
     (Just' x) >>= f = f x
     Nothing' >>= _ = Nothing'

   instance MonadPlus Maybe' where
     mzero = Nothing'
     mplus (Just' x) _ = Just' x
     mplus Nothing' y = y
   ```

53. **Implement a Simple HTTP Server:**
   Create a basic HTTP server that handles requests.
   ```haskell
   import Network.HTTP.Server
   import Network.HTTP.Server.Logger
   import Network.HTTP.Server.Response

   main :: IO ()
   main = do
     let config = serverConfig { serverPort = 8080 }
     serverWith config handleRequest

   handleRequest :: ServerRequest -> IO (Response String)
   handleRequest _ = return $ responseLBS status200 [] "Hello, Haskell!"
   ```

54. **Create a Simple Game Loop:**
   Implement a simple game loop that updates and renders game state.
   ```haskell
   import Control.Concurrent (threadDelay)

   main :: IO ()
   main = gameLoop initialState

   data GameState = GameState { playerPos :: Int }

   initialState :: GameState
   initialState = GameState 0

   gameLoop :: GameState -> IO ()
   gameLoop state = do
     render state
     let newState = update state
     threadDelay 100000 -- 100 ms delay
     gameLoop newState

   render :: GameState -> IO ()
   render state = putStrLn $ "Player position: " ++ show (playerPos state)

   update :: GameState -> GameState
   update state = state { playerPos = playerPos state + 1 }
   ```

55. **Pathfinding Algorithm:**
   Implement A* or Dijkstra's algorithm for pathfinding.
   ```haskell
   -- A simple implementation of Dijkstra's algorithm
   import Data.Map (Map)
   import qualified Data.Map as Map
   import Data.Maybe (fromMaybe)

   type Graph = Map String [(String, Int)]
   type Distances = Map String Int

   dijkstra :: Graph -> String -> Distances
   dijkstra graph start = dijkstra' graph (Map.singleton start 0) [start] Map.empty
     where
       dijkstra' _ distances [] _ = distances
       dijkstra' g dists (current:queue) visited =
         let (neighbors, newDists) = updateNeighbors g dists current
         in dijkstra' g newDists (queue ++ neighbors) (current : visited)

       updateNeighbors g dists current =
         let neighbors = Map.findWithDefault [] current g
             newDists = foldr update (dists) neighbors
             update (neighbor, weight) acc =
               let newDist = fromMaybe maxBound (Map.lookup current acc) + weight
               in if newDist < fromMaybe maxBound (Map.lookup neighbor acc)
                  then Map.insert neighbor newDist acc
                  else acc
         in (map fst neighbors, newDists)
   ```

56. **Type-Level Programming:**
   Experiment with type-level programming using GHC extensions.
   ```haskell
   {-# LANGUAGE DataKinds, TypeFamilies #-}

   data Nat = Zero | Succ Nat

   type family Add (m :: Nat) (n :: Nat) :: Nat where
     Add Zero n = n
     Add (Succ m) n = Succ (Add m n)

   type family Multiply (m :: Nat) (n :: Nat) :: Nat where
     Multiply Zero _ = Zero
     Multiply (Succ m) n = Add n (Multiply m n)
   ```

57. **Implement a DSL:**
   Create a simple domain-specific language (DSL) for a specific problem domain.
   ```haskell
   data Expr = Num Int | Add Expr Expr | Mul Expr Expr

   eval :: Expr -> Int
   eval (Num n) = n
   eval (Add e1 e2) = eval e1 + eval e2
   eval (Mul e1 e2) = eval e1 * eval e2

   example :: Expr
   example = Add (Num 5) (Mul (Num 2) (Num 3))
   ```

58. **Build a Simple REPL:**
   Implement a Read-Eval-Print Loop (REPL) for a mini-language.
   ```haskell
   import Control.Monad (forever)

   main :: IO ()
   main = forever $ do
     putStr "> "
     line <- getLine
     let result = eval line
     putStrLn result

   eval :: String -> String
   eval input = "You entered: " ++ input
   ```

59. **Implement `MonadReader`:**
   Define and implement the `MonadReader` type class.
   ```haskell
   import Control.Monad.Reader

   type Env = String

   hello :: Reader Env String
   hello = do
     name <- ask
     return $ "Hello, " ++ name ++ "!"

   runHello :: String -> String
   runHello name = runReader hello name
   ```

60. **Create a Simple ORM:**
   Implement a simple Object-Relational Mapping (ORM) system.
   ```haskell
   import Data.Map.Strict (Map)
   import qualified Data.Map.Strict as Map

   data User = User { userId :: Int, userName :: String } deriving Show

   type Database = Map Int User

   insertUser :: Int -> String -> Database -> Database
   insertUser uid name db = Map.insert uid (User uid name) db

   getUser :: Int -> Database -> Maybe User
   getUser uid db = Map.lookup uid db
   ```

61. **Tic-Tac-Toe Game:**
   Build a console-based Tic-Tac-Toe game.
   ```haskell
   import Data.List (intercalate)

   data Player = X | O deriving (Eq, Show)
   type Board = [[Maybe Player]]

   main :: IO ()
   main = gameLoop initialBoard X

   initialBoard :: Board
   initialBoard = replicate 3 (replicate 3 Nothing)

   gameLoop :: Board -> Player -> IO ()
   gameLoop board player = do
     putStrLn (showBoard board)
     move <- getLine
     let (row, col) = parseMove move
     let newBoard = makeMove board player (row, col)
     if checkWinner newBoard player
       then putStrLn (showBoard newBoard ++ "\n" ++ show player ++ " wins!")
       else gameLoop newBoard (nextPlayer player)

   showBoard :: Board -> String
   showBoard board = intercalate "\n" [concatMap showCell row | row <- board]
     where
       showCell Nothing = "_"
       showCell (Just X) = "X"
       showCell (Just O) = "O"

   parseMove :: String -> (Int, Int)
   parseMove move = (read [head move], read [last move]) -- e.g., "23" -> (2, 3)

   makeMove :: Board -> Player -> (Int, Int) -> Board
   makeMove board player (row, col) =
     [if r == row then replace col (Just player) row' else row' | (r, row') <- zip [0..] board]
     where
       replace c val row = take c row ++ [val] ++ drop (c + 1) row

   nextPlayer :: Player -> Player
   nextPlayer X = O
   nextPlayer O = X

   checkWinner :: Board -> Player -> Bool
   checkWinner board player = any (all (== Just player)) (rows ++ cols ++ diags)
     where
       rows = board
       cols = transpose board
       diags = [[board !! i !! i | i <- [0..2]], [board !! i !! (2-i) | i <- [0..2]]]
   ```

62. **Chat Application:**
   Create a simple chat application using sockets.
   ```haskell
   import Network.Socket
   import Network.Socket.ByteString (send, recv)
   import Control.Concurrent (forkIO)

   main :: IO ()
   main = do
     sock <- socket AF_INET Stream 0
     bind sock (SockAddrInet 8080 iNADDR_ANY)
     listen sock 1
     putStrLn "Listening on port 8080..."
     acceptConnections sock

   acceptConnections :: Socket -> IO ()
  

 acceptConnections sock = do
     (conn, _) <- accept sock
     putStrLn "Client connected"
     forkIO (handleClient conn)
     acceptConnections sock

   handleClient :: Socket -> IO ()
   handleClient conn = do
     msg <- recv conn 1024
     putStrLn ("Received: " ++ show msg)
     send conn msg
     handleClient conn
   ```

63. **File Compression:**
   Implement a basic file compression algorithm.
   ```haskell
   import Codec.Compression.GZip (compress, decompress)
   import qualified Data.ByteString.Lazy as B

   compressFile :: FilePath -> FilePath -> IO ()
   compressFile input output = do
     content <- B.readFile input
     B.writeFile output (compress content)

   decompressFile :: FilePath -> FilePath -> IO ()
   decompressFile input output = do
     content <- B.readFile input
     B.writeFile output (decompress content)
   ```

64. **Simple Database:**
   Create a simple in-memory database with basic CRUD operations.
   ```haskell
   import Data.Map.Strict (Map)
   import qualified Data.Map.Strict as Map

   data Record = Record { recordId :: Int, recordData :: String } deriving Show

   type Database = Map Int Record

   insertRecord :: Int -> String -> Database -> Database
   insertRecord rid data' db = Map.insert rid (Record rid data') db

   getRecord :: Int -> Database -> Maybe Record
   getRecord rid db = Map.lookup rid db

   deleteRecord :: Int -> Database -> Database
   deleteRecord rid db = Map.delete rid db

   updateRecord :: Int -> String -> Database -> Database
   updateRecord rid data' db = Map.adjust (\_ -> Record rid data') rid db
   ```

65. **Natural Language Processing:**
   Implement basic NLP tasks like tokenization or stemming.
   ```haskell
   import Data.List.Split (splitOn)

   tokenize :: String -> [String]
   tokenize text = splitOn " " text

   -- Example usage: tokenize "Hello world, how are you?"
   ```

66. **Blockchain Simulation:**
   Simulate a basic blockchain structure.
   ```haskell
   data Block = Block { index :: Int, previousHash :: String, data :: String } deriving Show

   type Blockchain = [Block]

   createGenesisBlock :: Block
   createGenesisBlock = Block 0 "0" "Genesis Block"

   addBlock :: Blockchain -> String -> Blockchain
   addBlock chain newData = Block (length chain) (hash lastBlock) newData : chain
     where lastBlock = head chain

   hash :: Block -> String
   hash (Block idx prevHash data) = show (idx + length prevHash + length data) -- Dummy hash function
   ```

67. **Build a Web Scraper:**
   Write a web scraper that extracts specific data from a webpage.
   ```haskell
   import Network.HTTP.Simple
   import Text.HTML.Scalaz
   import Text.HTML.TagSoup

   scrapeURL :: String -> IO [String]
   scrapeURL url = do
     response <- httpLBS url
     let body = getResponseBody response
         tags = parseTags (show body)
     return [innerText tag | tag <- tags, isTagOpenName "h1" tag]
   ```

68. **Implement a Simple Task Queue:**
   Create a simple task queue with worker threads.
   ```haskell
   import Control.Concurrent
   import Control.Concurrent.MVar

   type Task = Int

   main :: IO ()
   main = do
     queue <- newMVar []
     forkIO $ worker queue
     replicateM_ 10 (addTask queue 1)

   addTask :: MVar [Task] -> Task -> IO ()
   addTask queue task = modifyMVar_ queue $ \tasks -> return (tasks ++ [task])

   worker :: MVar [Task] -> IO ()
   worker queue = forever $ do
     tasks <- takeMVar queue
     case tasks of
       [] -> putMVar queue [] >> threadDelay 1000000
       (t:ts) -> do
         putStrLn $ "Processing task: " ++ show t
         putMVar queue ts
   ```

69. **Unit Testing:**
   Write unit tests for existing functions using a testing library.
   ```haskell
   import Test.HUnit

   add :: Int -> Int -> Int
   add x y = x + y

   testAdd :: Test
   testAdd = TestCase (assertEqual "for (add 1 2)," 3 (add 1 2))

   main :: IO ()
   main = runTestTT testAdd >> return ()
   ```

70. **Implement a State Machine:**
   Create a finite state machine for a simple use case.
   ```haskell
   data State = Start | StateA | StateB | End deriving (Show)

   data Transition = Transition State State deriving (Show)

   transition :: Transition -> State -> State
   transition (Transition Start StateA) Start = StateA
   transition (Transition StateA StateB) StateA = StateB
   transition (Transition StateB End) StateB = End
   transition _ currentState = currentState
   ```

71. **Create a Scheduler:**
   Implement a task scheduler that executes tasks at specified intervals.
   ```haskell
   import Control.Concurrent (forkIO, threadDelay)

   type Task = IO ()

   main :: IO ()
   main = do
     let task = putStrLn "Task executed"
     forkIO $ scheduler task 1000000 -- Execute every second
     putStrLn "Scheduler started"
     threadDelay 5000000 -- Keep main thread alive for 5 seconds

   scheduler :: Task -> Int -> IO ()
   scheduler task interval = forever $ do
     task
     threadDelay interval
   ```

72. **Event Sourcing:**
   Build a simple event-sourced application.
   ```haskell
   data Event = UserCreated String | UserDeleted String deriving Show

   type EventStore = [Event]

   addEvent :: Event -> EventStore -> EventStore
   addEvent event store = event : store

   applyEvents :: EventStore -> [String]
   applyEvents = map applyEvent
     where
       applyEvent (UserCreated name) = "User created: " ++ name
       applyEvent (UserDeleted name) = "User deleted: " ++ name
   ```

73. **LSTM Implementation:**
   Implement a basic Long Short-Term Memory (LSTM) neural network from scratch.
   ```haskell
   -- This is a complex task; a full implementation would require
   -- a significant amount of code. Instead, a simplified version is shown.
   data LSTM = LSTM { forgetGate :: [Double], inputGate :: [Double], outputGate :: [Double] }

   -- Example of creating an LSTM
   initLSTM :: Int -> LSTM
   initLSTM size = LSTM (replicate size 0) (replicate size 0) (replicate size 0)
   ```

74. **Design Patterns:**
   Implement common design patterns (e.g., Singleton, Factory) in Haskell.
   ```haskell
   -- Singleton pattern
   import Data.IORef

   data Singleton = Singleton { value :: Int }

   getInstance :: IO (IORef Singleton)
   getInstance = newIORef (Singleton 42)

   -- Factory pattern
   data Shape = Circle Double | Rectangle Double Double deriving Show

   createShape :: String -> [Double] -> Maybe Shape
   createShape "circle" [r] = Just (Circle r)
   createShape "rectangle" [w, h] = Just (Rectangle w h)
   createShape _ _ = Nothing
   ```

75. **Code Generator:**
   Write a code generator that generates Haskell code based on input specifications.
   ```haskell
   generateFunction :: String -> String
   generateFunction name = "myFunc :: Int -> Int\n" ++
                            "myFunc x = x + 1 -- Function: " ++ name

   main :: IO ()
   main = do
     let code = generateFunction "Increment"
     putStrLn code
  ```

---

Here are the solutions to the Scala exercises for beginners (1-25), including explanations and code snippets for each exercise.

### Scala Exercises Solutions

#### Beginner (1-25)

1. **Factorial Calculation:**
   Implement a recursive function to calculate the factorial of a number.
   ```scala
   def factorial(n: Int): Int = {
     if (n <= 1) 1
     else n * factorial(n - 1)
   }
   ```

2. **Fibonacci Sequence:**
   Write a function to generate the nth Fibonacci number.
   ```scala
   def fibonacci(n: Int): Int = {
     if (n <= 1) n
     else fibonacci(n - 1) + fibonacci(n - 2)
   }
   ```

3. **Palindrome Checker:**
   Create a function to check if a given string is a palindrome.
   ```scala
   def isPalindrome(s: String): Boolean = {
     s == s.reverse
   }
   ```

4. **Sum of Squares:**
   Implement a function to compute the sum of squares of a list of integers.
   ```scala
   def sumOfSquares(numbers: List[Int]): Int = {
     numbers.map(n => n * n).sum
   }
   ```

5. **List Reversal:**
   Write a function to reverse a list without using built-in functions.
   ```scala
   def reverseList[T](list: List[T]): List[T] = {
     def loop(lst: List[T], acc: List[T]): List[T] = lst match {
       case Nil => acc
       case head :: tail => loop(tail, head :: acc)
     }
     loop(list, Nil)
   }
   ```

6. **Filter Even Numbers:**
   Implement a function to filter out even numbers from a list.
   ```scala
   def filterEven(numbers: List[Int]): List[Int] = {
     numbers.filter(_ % 2 != 0)
   }
   ```

7. **Merge Sort:**
   Create an implementation of the merge sort algorithm.
   ```scala
   def mergeSort[T](list: List[T])(implicit ord: Ordering[T]): List[T] = {
     if (list.length <= 1) list
     else {
       val (left, right) = list.splitAt(list.length / 2)
       merge(mergeSort(left), mergeSort(right))
     }
   }

   def merge[T](left: List[T], right: List[T])(implicit ord: Ordering[T]): List[T] = {
     (left, right) match {
       case (Nil, _) => right
       case (_, Nil) => left
       case (lHead :: lTail, rHead :: rTail) =>
         if (ord.lteq(lHead, rHead)) lHead :: merge(lTail, right)
         else rHead :: merge(left, rTail)
     }
   }
   ```

8. **Matrix Multiplication:**
   Implement matrix multiplication for 2x2 matrices.
   ```scala
   def matrixMultiply(a: Array[Array[Int]], b: Array[Array[Int]]): Array[Array[Int]] = {
     Array(
       Array(a(0)(0) * b(0)(0) + a(0)(1) * b(1)(0), a(0)(0) * b(0)(1) + a(0)(1) * b(1)(1)),
       Array(a(1)(0) * b(0)(0) + a(1)(1) * b(1)(0), a(1)(0) * b(0)(1) + a(1)(1) * b(1)(1))
     )
   }
   ```

9. **Define a Trait and Implement:**
   Define a trait `Shape` with methods for area and perimeter. Implement this trait for `Circle` and `Rectangle`.
   ```scala
   trait Shape {
     def area: Double
     def perimeter: Double
   }

   class Circle(radius: Double) extends Shape {
     def area: Double = Math.PI * radius * radius
     def perimeter: Double = 2 * Math.PI * radius
   }

   class Rectangle(width: Double, height: Double) extends Shape {
     def area: Double = width * height
     def perimeter: Double = 2 * (width + height)
   }
   ```

10. **File I/O:**
    Write a function to count the number of lines in a file.
    ```scala
    import scala.io.Source

    def countLines(filename: String): Int = {
      val source = Source.fromFile(filename)
      try source.getLines().size finally source.close()
    }
    ```

11. **Parse JSON Data:**
    Use a JSON library (e.g., `play-json`) to parse JSON data and extract specific fields.
    ```scala
    import play.api.libs.json._

    def parseJson(jsonString: String): Option[String] = {
      val json: JsValue = Json.parse(jsonString)
      (json \ "name").asOpt[String] // Extract the "name" field
    }
    ```

12. **Generate Primes:**
    Write a function to generate all prime numbers up to a given number using the Sieve of Eratosthenes.
    ```scala
    def sieveOfEratosthenes(n: Int): List[Int] = {
      val sieve = Array.fill(n + 1)(true)
      for (i <- 2 to Math.sqrt(n).toInt if sieve(i)) {
        for (j <- i * i to n by i) {
          sieve(j) = false
        }
      }
      (2 to n).filter(sieve).toList
    }
    ```

13. **Custom Collection Class:**
    Implement a custom collection class that behaves like a stack with `push`, `pop`, and `peek` methods.
    ```scala
    class Stack[T] {
      private var elements: List[T] = Nil

      def push(element: T): Unit = {
        elements = element :: elements
      }

      def pop(): Option[T] = {
        elements match {
          case head :: tail =>
            elements = tail
            Some(head)
          case Nil => None
        }
      }

      def peek(): Option[T] = elements.headOption
    }
    ```

14. **Convert to Roman Numerals:**
    Implement a function that converts an integer to a Roman numeral.
    ```scala
    def intToRoman(num: Int): String = {
      val romanNumerals = List(
        1000 -> "M",
        900 -> "CM",
        500 -> "D",
        400 -> "CD",
        100 -> "C",
        90 -> "XC",
        50 -> "L",
        40 -> "XL",
        10 -> "X",
        9 -> "IX",
        5 -> "V",
        4 -> "IV",
        1 -> "I"
      )

      def loop(n: Int, acc: String): String = {
        if (n == 0) acc
        else {
          romanNumerals.find { case (value, _) => n >= value } match {
            case Some((value, numeral)) => loop(n - value, acc + numeral)
            case None => acc
          }
        }
      }

      loop(num, "")
    }
    ```

15. **Concurrency with Futures:**
    Use Scala’s `Future` to perform concurrent computations and combine results.
    ```scala
    import scala.concurrent.{Future, Await}
    import scala.concurrent.duration._
    import scala.concurrent.ExecutionContext.Implicits.global

    def computeFutures(): Unit = {
      val future1 = Future { 1 + 1 }
      val future2 = Future { 2 + 2 }

      val combinedFuture = for {
        result1 <- future1
        result2 <- future2
      } yield result1 + result2

      val result = Await.result(combinedFuture, 5.seconds)
      println(result) // Outputs: 6
    }
    ```

16. **Pattern Matching:**
    Write a function that uses pattern matching to decode a simple algebraic data type.
    ```scala
    sealed trait Expr
    case class Number(value: Int) extends Expr
    case class Add(left: Expr, right: Expr) extends Expr
    case class Multiply(left: Expr, right: Expr) extends Expr

    def eval(expr: Expr): Int = expr match {
      case Number(value) => value
      case Add(left, right) => eval(left) + eval(right)
      case Multiply(left, right) => eval(left) * eval(right)
    }
    ```

17. **Create an Actor System:**
    Use Akka to create a basic actor system with actors that send messages to each other.
    ```scala
    import akka.actor.{Actor, ActorSystem, Props}

    class Greeter extends Actor {
      def receive: Receive = {
        case "greet" => println("Hello!")
      }
    }

    object ActorSystemExample extends App {
      val system = ActorSystem("MyActorSystem")
      val greeter = system.actorOf(Props[Greeter], "greeter")
      greeter ! "greet"
      system.terminate()
    }
    ```

18. **Implement a Monad:**
    Define and implement a custom monad in Scala, demonstrating basic monadic operations.
    ```scala
    case class Box[A](value: A) {
      def map[B](f: A => B): Box[B] = Box(f(value))
      def flatMap[B](f: A => Box[B]): Box[B] = f(value)
    }



    // Example usage:
    val boxedValue = Box(5)
    val result = boxedValue.map(_ * 2).flatMap(v => Box(v + 3)) // Box(13)
    ```

19. **Software Transactional Memory:**
    Use `scala.concurrent.stm` to manage a shared counter with concurrent updates.
    ```scala
    import scala.concurrent.stm._

    def atomicCounterExample(): Unit = {
      val counter = Ref(0)

      val increments = List.fill(100)(Future {
        atomic { implicit txn =>
          counter.transform(_ + 1)
        }
      })

      Await.result(Future.sequence(increments), 10.seconds)
      println(counter.single()) // Outputs the final counter value
    }
    ```

20. **Property-Based Testing:**
    Write property-based tests using a library like `ScalaCheck` to test functions and properties.
    ```scala
    import org.scalacheck.Properties
    import org.scalacheck.Prop.forAll

    object MyProperties extends Properties("MyProperties") {
      property("sum of squares") = forAll { (a: Int, b: Int) =>
        sumOfSquares(List(a, b)) == (a * a + b * b)
      }
    }
    ```

21. **Count Vowels:**
    Create a function that counts the number of vowels in a string.
    ```scala
    def countVowels(s: String): Int = {
      s.count(c => "aeiouAEIOU".contains(c))
    }
    ```

22. **Find Maximum:**
    Write a function to find the maximum value in a list.
    ```scala
    def findMax(numbers: List[Int]): Int = {
      numbers.max
    }
    ```

23. **Generate Combinations:**
    Implement a function to generate all combinations of a list.
    ```scala
    def combinations[T](list: List[T]): List[List[T]] = {
      list.foldRight(List(List.empty[T]))((elem, acc) =>
        acc ++ acc.map(elem :: _)
      )
    }
    ```

24. **Count Words:**
    Create a function to count the number of words in a string.
    ```scala
    def countWords(s: String): Int = {
      s.split("\\s+").length
    }
    ```

25. **Flatten a List:**
    Implement a function to flatten a list of lists.
    ```scala
    def flatten[T](lists: List[List[T]]): List[T] = {
      lists.flatten
    }
    ```

#### **Intermediate (26-50)**

Here are the solutions to the Scala exercises from 26 to 50, covering a variety of topics including algorithms, data structures, and more advanced concepts.

### Scala Exercises Solutions (Continued)

#### 26-50

26. **Binary Search:**
   Implement a binary search algorithm.
   ```scala
   def binarySearch(arr: Array[Int], target: Int): Int = {
     def search(low: Int, high: Int): Int = {
       if (low > high) -1
       else {
         val mid = low + (high - low) / 2
         if (arr(mid) == target) mid
         else if (arr(mid) < target) search(mid + 1, high)
         else search(low, mid - 1)
       }
     }
     search(0, arr.length - 1)
   }
   ```

27. **Balanced Parentheses:**
   Write a function to check if parentheses in a string are balanced.
   ```scala
   def areBalanced(s: String): Boolean = {
     val stack = scala.collection.mutable.Stack[Char]()
     for (char <- s) {
       char match {
         case '(' => stack.push('(')
         case ')' =>
           if (stack.isEmpty || stack.pop() != '(') return false
         case _ => // ignore other characters
       }
     }
     stack.isEmpty
   }
   ```

28. **Unique Elements:**
   Implement a function to remove duplicate elements from a list.
   ```scala
   def uniqueElements[T](list: List[T]): List[T] = {
     list.distinct
   }
   ```

29. **Zip Lists:**
   Create a function to zip two lists into a list of tuples.
   ```scala
   def zipLists[A, B](list1: List[A], list2: List[B]): List[(A, B)] = {
     list1.zip(list2)
   }
   ```

30. **Longest Common Prefix:**
   Write a function that finds the longest common prefix in a list of strings.
   ```scala
   def longestCommonPrefix(strs: List[String]): String = {
     if (strs.isEmpty) return ""
     val prefix = new StringBuilder
     for (i <- 0 until strs.head.length) {
       val char = strs.head.charAt(i)
       if (strs.forall(_.length > i) && strs.forall(_.charAt(i) == char)) {
         prefix.append(char)
       } else {
         return prefix.toString()
       }
     }
     prefix.toString()
   }
   ```

31. **Nth Largest Element:**
   Implement a function to find the nth largest element in a list.
   ```scala
   def nthLargest(numbers: List[Int], n: Int): Option[Int] = {
     if (n <= 0 || n > numbers.distinct.size) None
     else Some(numbers.distinct.sorted(Ordering[Int].reverse)(n - 1))
   }
   ```

32. **Anagram Checker:**
   Write a function to check if two strings are anagrams.
   ```scala
   def areAnagrams(s1: String, s2: String): Boolean = {
     s1.sorted == s2.sorted
   }
   ```

33. **Group Anagrams:**
   Implement a function to group anagrams from a list of strings.
   ```scala
   def groupAnagrams(strs: List[String]): List[List[String]] = {
     strs.groupBy(_.sorted).values.toList
   }
   ```

34. **Count Characters:**
   Write a function that counts the occurrences of each character in a string.
   ```scala
   def countCharacters(s: String): Map[Char, Int] = {
     s.groupBy(identity).mapValues(_.length)
   }
   ```

35. **Transpose a Matrix:**
   Implement a function to transpose a given matrix.
   ```scala
   def transpose(matrix: Array[Array[Int]]): Array[Array[Int]] = {
     val rows = matrix.length
     val cols = matrix(0).length
     Array.tabulate(cols, rows)((i, j) => matrix(j)(i))
   }
   ```

36. **Find the Mode:**
   Write a function to find the mode of a list.
   ```scala
   def findMode(numbers: List[Int]): List[Int] = {
     val grouped = numbers.groupBy(identity).mapValues(_.size)
     val maxCount = grouped.values.max
     grouped.filter(_._2 == maxCount).keys.toList
   }
   ```

37. **Sort by Frequency:**
   Write a function to sort a list of elements by their frequency of occurrence.
   ```scala
   def sortByFrequency[T](list: List[T]): List[T] = {
     list.groupBy(identity).toList.sortBy(-_._2.size).flatMap(_._2)
   }
   ```

38. **Implement a Simple HTTP Client:**
   Use a library to implement a simple HTTP client that fetches data from a URL.
   ```scala
   import scala.io.Source
   import scala.util.Try

   def fetchUrl(url: String): Try[String] = {
     Try {
       val source = Source.fromURL(url)
       try source.mkString finally source.close()
     }
   }
   ```

39. **Basic HTTP Server:**
   Create a basic HTTP server that handles requests.
   ```scala
   import java.net.{ServerSocket, Socket}
   import java.io.PrintWriter

   object SimpleHttpServer {
     def main(args: Array[String]): Unit = {
       val server = new ServerSocket(8080)
       while (true) {
         val client: Socket = server.accept()
         handleRequest(client)
       }
     }

     def handleRequest(client: Socket): Unit = {
       val out = new PrintWriter(client.getOutputStream, true)
       out.println("HTTP/1.1 200 OK")
       out.println("Content-Type: text/plain")
       out.println()
       out.println("Hello, World!")
       out.close()
       client.close()
     }
   }
   ```

40. **Basic Logging Framework:**
   Implement a simple logging framework that writes log messages to a file.
   ```scala
   import java.io.{File, PrintWriter}

   object Logger {
     private val file = new File("log.txt")
     private val writer = new PrintWriter(file)

     def log(message: String): Unit = {
       writer.println(message)
       writer.flush()
     }

     def close(): Unit = {
       writer.close()
     }
   }
   ```

41. **Event Loop:**
   Create a simple event loop that processes events from a queue.
   ```scala
   import scala.collection.mutable.Queue

   class EventLoop {
     private val events = Queue[String]()

     def enqueue(event: String): Unit = {
       events.enqueue(event)
     }

     def processEvents(): Unit = {
       while (events.nonEmpty) {
         val event = events.dequeue()
         println(s"Processing event: $event")
       }
     }
   }
   ```

42. **Implement `Functor`:**
   Define and implement the `Functor` type class for a custom type.
   ```scala
   trait Functor[F[_]] {
     def map[A, B](fa: F[A])(f: A => B): F[B]
   }

   case class Box[A](value: A)

   implicit val boxFunctor: Functor[Box] = new Functor[Box] {
     def map[A, B](fa: Box[A])(f: A => B): Box[B] = Box(f(fa.value))
   }
   ```

43. **Memoization:**
   Write a memoization function to optimize recursive computations.
   ```scala
   def memoize[A, B](f: A => B): A => B = {
     val cache = scala.collection.mutable.Map.empty[A, B]
     (x: A) => cache.getOrElseUpdate(x, f(x))
   }

   // Example usage:
   val fib: Int => Int = memoize(n => if (n <= 1) n else fib(n - 1) + fib(n - 2))
   ```

44. **Create a State Monad:**
   Implement a simple state monad and demonstrate its use.
   ```scala
   case class State[S, A](run: S => (A, S)) {
     def map[B](f: A => B): State[S, B] = State(s => {
       val (a, newState) = run(s)
       (f(a), newState)
     })

     def flatMap[B](f: A => State[S, B]): State[S, B] = State(s => {
       val (a, newState) = run(s)
       f(a).run(newState)
     })
   }

   // Example usage:
   def increment: State[Int, Int] = State(s => (s, s + 1))
   ```

45. **Implement a Simple DSL:**
   Create a simple domain-specific language (DSL) for a specific problem domain.
   ```scala
   case class Command(name: String, args: List[String])

   object DSL {
     def run(command: Command): Unit = {
       command.name match {
         case "print" => println(command.args.mkString(" "))
         case _ => println("Unknown command")
       }
     }

     def print(args: String*): Command = Command("print", args.toList)
   }

   // Example usage:
   DSL.run(DSL.print("Hello", "DSL"))
   ```

46. **Tic-Tac-Toe Game:**
   Build a console-based Tic-Tac-Toe game.
   ```scala
   class TicTacToe

 {
     private val board = Array.fill(3, 3)(' ')

     def play(): Unit = {
       var currentPlayer = 'X'
       for (turn <- 1 to 9) {
         printBoard()
         println(s"Player $currentPlayer, enter your move (row and column):")
         val Array(row, col) = scala.io.StdIn.readLine().split(" ").map(_.toInt)
         if (board(row)(col) == ' ') {
           board(row)(col) = currentPlayer
           if (checkWinner(currentPlayer)) {
             printBoard()
             println(s"Player $currentPlayer wins!")
             return
           }
           currentPlayer = if (currentPlayer == 'X') 'O' else 'X'
         } else {
           println("Invalid move, try again.")
           turn -= 1
         }
       }
       printBoard()
       println("It's a draw!")
     }

     private def checkWinner(player: Char): Boolean = {
       (0 until 3).exists(row => board(row).forall(_ == player)) || // rows
       (0 until 3).exists(col => board.forall(_(col) == player)) || // columns
       (0 until 3).forall(i => board(i)(i) == player) || // diagonal \
       (0 until 3).forall(i => board(i)(2 - i) == player) // diagonal /
     }

     private def printBoard(): Unit = {
       board.foreach(row => println(row.mkString("|")))
       println("-" * 5)
     }
   }

   // Example usage:
   // new TicTacToe().play()
   ```

47. **File Compression:**
   Implement a basic file compression algorithm (e.g., RLE).
   ```scala
   def compress(input: String): String = {
     val sb = new StringBuilder
     var count = 1

     for (i <- 1 until input.length) {
       if (input(i) == input(i - 1)) count += 1
       else {
         sb.append(input(i - 1)).append(count)
         count = 1
       }
     }
     sb.append(input.last).append(count)
     sb.toString()
   }
   ```

48. **Unit Testing:**
   Write unit tests for existing functions using a testing library.
   ```scala
   import org.scalatest.flatspec.AnyFlatSpec
   import org.scalatest.matchers.should.Matchers

   class MyTests extends AnyFlatSpec with Matchers {
     "An anagram checker" should "return true for anagrams" in {
       areAnagrams("listen", "silent") should be(true)
     }

     it should "return false for non-anagrams" in {
       areAnagrams("hello", "world") should be(false)
     }
   }
   ```

49. **Create a Custom Exception:**
   Implement a custom exception class and demonstrate its use.
   ```scala
   class CustomException(message: String) extends Exception(message)

   def mayThrowException(): Unit = {
     throw new CustomException("This is a custom exception!")
   }

   try {
     mayThrowException()
   } catch {
     case e: CustomException => println(e.getMessage)
   }
   ```

50. **Basic CRUD Application:**
   Build a simple console-based CRUD application.
   ```scala
   case class Item(id: Int, name: String)

   object CRUDApp {
     private var items = List.empty[Item]
     private var nextId = 1

     def create(name: String): Unit = {
       items = items :+ Item(nextId, name)
       nextId += 1
       println(s"Created: $name")
     }

     def read(): Unit = {
       println("Items:")
       items.foreach(item => println(s"${item.id}: ${item.name}"))
     }

     def update(id: Int, newName: String): Unit = {
       items = items.map {
         case Item(`id`, _) => Item(id, newName)
         case other => other
       }
       println(s"Updated item $id to $newName")
     }

     def delete(id: Int): Unit = {
       items = items.filterNot(_.id == id)
       println(s"Deleted item $id")
     }

     def main(args: Array[String]): Unit = {
       create("Item 1")
       create("Item 2")
       read()
       update(1, "Updated Item 1")
       delete(2)
       read()
     }
   }
   ```

#### **Advanced (51-75)**

Here are the solutions for exercises 51 to 75 in Scala, encompassing algorithms, design patterns, web applications, and more advanced concepts. 

### Scala Exercises Solutions (51-75)

#### 51-75

51. **Quicksort Algorithm:**
   Implement the quicksort algorithm.
   ```scala
   def quicksort[T](list: List[T])(implicit ord: Ordering[T]): List[T] = {
     if (list.isEmpty) {
       list
     } else {
       val pivot = list.head
       val (less, greater) = list.tail.partition(ord.lt(_, pivot))
       quicksort(less) ::: pivot :: quicksort(greater)
     }
   }
   ```

52. **Implement `MonadPlus`:**
   Define and implement the `MonadPlus` type class.
   ```scala
   trait Monad[M[_]] {
     def flatMap[A, B](ma: M[A])(f: A => M[B]): M[B]
     def pure[A](a: A): M[A]
   }

   trait MonadPlus[M[_]] extends Monad[M] {
     def empty[A]: M[A]
     def combine[A](ma: M[A], mb: M[A]): M[A]
   }

   case class OptionMonadPlus() extends MonadPlus[Option] {
     def flatMap[A, B](ma: Option[A])(f: A => Option[B]): Option[B] = ma.flatMap(f)
     def pure[A](a: A): Option[A] = Some(a)
     def empty[A]: Option[A] = None
     def combine[A](ma: Option[A], mb: Option[A]): Option[A] = ma.orElse(mb)
   }
   ```

53. **Chat Application:**
   Create a simple chat application using sockets.
   ```scala
   import java.net.{ServerSocket, Socket}
   import java.io.{BufferedReader, InputStreamReader, PrintWriter}

   object ChatServer {
     def main(args: Array[String]): Unit = {
       val server = new ServerSocket(9999)
       println("Chat server started on port 9999.")
       while (true) {
         val client: Socket = server.accept()
         new Thread(() => handleClient(client)).start()
       }
     }

     def handleClient(client: Socket): Unit = {
       val in = new BufferedReader(new InputStreamReader(client.getInputStream))
       val out = new PrintWriter(client.getOutputStream, true)

       out.println("Welcome to the chat!")
       var message: String = ""
       while ({ message = in.readLine(); message != null }) {
         println(s"Received: $message")
         out.println(s"Echo: $message")
       }
       client.close()
     }
   }
   ```

54. **Pathfinding Algorithm:**
   Implement A* or Dijkstra's algorithm for pathfinding (Dijkstra's example).
   ```scala
   import scala.collection.mutable

   case class Edge(destination: Int, weight: Int)
   type Graph = Map[Int, List[Edge]]

   def dijkstra(graph: Graph, start: Int): Map[Int, Int] = {
     val distances = mutable.Map(graph.keys.toSeq.map(_ -> Int.MaxValue): _*)
     distances(start) = 0
     val priorityQueue = mutable.PriorityQueue[(Int, Int)]()(Ordering.by(-_._2))

     priorityQueue.enqueue((start, 0))

     while (priorityQueue.nonEmpty) {
       val (node, dist) = priorityQueue.dequeue()
       if (dist <= distances(node)) {
         graph.getOrElse(node, List()).foreach { edge =>
           val newDist = dist + edge.weight
           if (newDist < distances(edge.destination)) {
             distances(edge.destination) = newDist
             priorityQueue.enqueue((edge.destination, newDist))
           }
         }
       }
     }
     distances.toMap
   }
   ```

55. **Type-Level Programming:**
   Experiment with type-level programming using Scala's advanced features.
   ```scala
   // Type-level programming can be complex and is often an advanced topic. Here's a simple example using type classes.
   trait Show[A] {
     def show(a: A): String
   }

   implicit val intShow: Show[Int] = (a: Int) => a.toString
   implicit val stringShow: Show[String] = (a: String) => a

   def showValue[A](value: A)(implicit s: Show[A]): String = s.show(value)

   // Example usage:
   // println(showValue(42)) // Output: "42"
   // println(showValue("Hello")) // Output: "Hello"
   ```

56. **Implement a Simple Task Queue:**
   Create a simple task queue with worker threads.
   ```scala
   import scala.collection.mutable.Queue
   import scala.concurrent.{ExecutionContext, Future}
   import scala.concurrent.ExecutionContext.Implicits.global

   class TaskQueue {
     private val queue = Queue[() => Unit]()

     def addTask(task: () => Unit): Unit = {
       queue.enqueue(task)
       processTasks()
     }

     private def processTasks(): Unit = {
       while (queue.nonEmpty) {
         val task = queue.dequeue()
         Future(task())
       }
     }
   }

   // Example usage:
   // val taskQueue = new TaskQueue
   // taskQueue.addTask(() => println("Task 1 completed"))
   // taskQueue.addTask(() => println("Task 2 completed"))
   ```

57. **Build a Web Scraper:**
   Write a web scraper that extracts specific data from a webpage.
   ```scala
   import org.jsoup.Jsoup

   object WebScraper {
     def scrape(url: String): Unit = {
       val doc = Jsoup.connect(url).get()
       val titles = doc.select("h1, h2, h3").eachText()
       println("Extracted Titles:")
       titles.forEach(title => println(title))
     }

     // Example usage:
     // scrape("https://example.com")
   }
   ```

58. **Natural Language Processing:**
   Implement basic NLP tasks like tokenization or stemming.
   ```scala
   object NLP {
     def tokenize(text: String): List[String] = {
       text.split("\\W+").toList
     }

     // Example usage:
     // val tokens = tokenize("Hello, world! This is a test.")
     // println(tokens) // Output: List("Hello", "world", "This", "is", "a", "test")
   }
   ```

59. **Implement a State Machine:**
   Create a finite state machine for a simple use case.
   ```scala
   sealed trait State
   case object On extends State
   case object Off extends State

   class Light {
     private var state: State = Off

     def toggle(): Unit = {
       state = state match {
         case Off => On
         case On => Off
       }
       println(s"Light is now: $state")
     }
   }

   // Example usage:
   // val light = new Light
   // light.toggle() // Light is now: On
   // light.toggle() // Light is now: Off
   ```

60. **Simple Event Sourcing:**
   Build a simple event-sourced application.
   ```scala
   case class Event(name: String)

   class EventStore {
     private var events = List.empty[Event]

     def addEvent(event: Event): Unit = {
       events = event :: events
     }

     def getEvents: List[Event] = events
   }

   // Example usage:
   // val store = new EventStore
   // store.addEvent(Event("Created item"))
   // store.getEvents.foreach(e => println(e.name))
   ```

61. **Implement a Simple ORM:**
   Create a simple Object-Relational Mapping (ORM) system.
   ```scala
   case class User(id: Int, name: String)

   object ORM {
     private var db = Map.empty[Int, User]

     def save(user: User): Unit = {
       db += (user.id -> user)
     }

     def find(id: Int): Option[User] = {
       db.get(id)
     }
   }

   // Example usage:
   // ORM.save(User(1, "Alice"))
   // println(ORM.find(1)) // Output: Some(User(1, "Alice"))
   ```

62. **Blockchain Simulation:**
   Simulate a basic blockchain structure.
   ```scala
   case class Block(index: Int, previousHash: String, data: String)

   object Blockchain {
     private var chain: List[Block] = List()

     def createBlock(data: String): Block = {
       val index = chain.length
       val previousHash = if (chain.isEmpty) "0" else chain.last.previousHash
       val block = Block(index, previousHash, data)
       chain = block :: chain
       block
     }

     def getChain: List[Block] = chain.reverse
   }

   // Example usage:
   // Blockchain.createBlock("Genesis Block")
   // Blockchain.createBlock("Second Block")
   // Blockchain.getChain.foreach(b => println(b))
   ```

63. **LSTM Implementation:**
   Implement a basic Long Short-Term Memory (LSTM) neural network from scratch.
   ```scala
   // Implementing an LSTM from scratch is quite complex. Here's a simplified version of its structure.
   case class LSTM(inputSize: Int, hiddenSize: Int) {
     private val Wf = Array.fill(hiddenSize, inputSize)(0.0) // Forget gate weights
     private val Wi = Array.fill(hiddenSize, inputSize)(0.0) // Input gate weights
     private val Wc = Array.fill(hiddenSize, input

Size)(0.0) // Cell gate weights
     private val Wo = Array.fill(hiddenSize, inputSize)(0.0) // Output gate weights

     // LSTM step function can be implemented here
     def step(input: Array[Double]): Array[Double] = {
       // Placeholder for the actual LSTM logic
       input.map(_ * 0.5) // Dummy operation
     }
   }

   // Example usage:
   // val lstm = LSTM(10, 20)
   // val output = lstm.step(Array.fill(10)(1.0))
   ```

64. **Create a Simple Game Loop:**
   Implement a simple game loop that updates and renders game state.
   ```scala
   import scala.concurrent.duration._
   import scala.concurrent.ExecutionContext.Implicits.global
   import scala.concurrent.Future
   import scala.util.Random

   class Game {
     private var running = true
     private var state = "Start"

     def update(): Unit = {
       state = if (Random.nextBoolean()) "Running" else "Paused"
     }

     def render(): Unit = {
       println(s"Game State: $state")
     }

     def run(): Unit = {
       Future {
         while (running) {
           update()
           render()
           Thread.sleep(1000)
         }
       }
     }

     def stop(): Unit = running = false
   }

   // Example usage:
   // val game = new Game
   // game.run()
   ```

65. **Design Patterns:**
   Implement common design patterns (e.g., Singleton, Factory) in Scala.
   ```scala
   object Singleton {
     private var instance: Option[Singleton] = None
     def getInstance: Singleton = {
       if (instance.isEmpty) {
         instance = Some(new Singleton)
       }
       instance.get
     }
   }

   class Singleton private() // private constructor

   object Factory {
     def createAnimal(animalType: String): Animal = {
       animalType match {
         case "Dog" => new Dog
         case "Cat" => new Cat
         case _ => throw new IllegalArgumentException("Unknown animal type")
       }
     }
   }

   trait Animal {
     def speak(): String
   }

   class Dog extends Animal {
     def speak(): String = "Woof!"
   }

   class Cat extends Animal {
     def speak(): String = "Meow!"
   }
   ```

66. **Custom Data Structure:**
   Implement a custom data structure (e.g., a trie or a graph).
   ```scala
   class TrieNode {
     var children: Map[Char, TrieNode] = Map()
     var isEndOfWord: Boolean = false
   }

   class Trie {
     private val root = new TrieNode

     def insert(word: String): Unit = {
       var currentNode = root
       for (char <- word) {
         currentNode.children.getOrElseUpdate(char, new TrieNode())
         currentNode = currentNode.children(char)
       }
       currentNode.isEndOfWord = true
     }

     def search(word: String): Boolean = {
       var currentNode = root
       for (char <- word) {
         currentNode.children.get(char) match {
           case Some(node) => currentNode = node
           case None => return false
         }
       }
       currentNode.isEndOfWord
     }
   }

   // Example usage:
   // val trie = new Trie
   // trie.insert("hello")
   // println(trie.search("hello")) // Output: true
   // println(trie.search("hell")) // Output: false
   ```

67. **Build a Simple API:**
   Create a RESTful API using a web framework (e.g., Akka HTTP).
   ```scala
   import akka.http.scaladsl.Http
   import akka.http.scaladsl.model._
   import akka.http.scaladsl.server.Directives._
   import akka.actor.ActorSystem
   import akka.stream.ActorMaterializer

   object SimpleApi {
     implicit val system = ActorSystem("my-system")
     implicit val materializer = ActorMaterializer()
     implicit val executionContext = system.dispatcher

     def main(args: Array[String]): Unit = {
       val route =
         path("hello") {
           get {
             complete(HttpEntity(ContentTypes.`text/plain(UTF-8)`, "Hello, World!"))
           }
         }

       Http().bindAndHandle(route, "localhost", 8080)
       println("Server online at http://localhost:8080/")
     }
   }
   ```

68. **Basic Chatbot:**
   Implement a simple rule-based chatbot.
   ```scala
   object Chatbot {
     def respond(input: String): String = {
       input.toLowerCase match {
         case "hello" => "Hi there!"
         case "how are you?" => "I'm just a computer program, but thanks for asking!"
         case "bye" => "Goodbye!"
         case _ => "I'm not sure how to respond to that."
       }
     }

     // Example usage:
     // println(respond("hello")) // Output: Hi there!
   }
   ```

69. **Unit Testing:**
   Write unit tests for existing functions using a testing library.
   ```scala
   import org.scalatest.flatspec.AnyFlatSpec
   import org.scalatest.matchers.should.Matchers

   class MathTests extends AnyFlatSpec with Matchers {
     "The sum function" should "return the correct sum of two numbers" in {
       assert(sum(1, 2) == 3)
       assert(sum(-1, 1) == 0)
     }
   }

   def sum(a: Int, b: Int): Int = a + b
   ```

70. **Implement Reactive Programming:**
   Use a reactive programming library to build a simple application (e.g., using RxScala).
   ```scala
   import rx.lang.scala.Observable

   object ReactiveApp {
     def main(args: Array[String]): Unit = {
       val numbers = Observable.range(1, 10)
       numbers.map(_ * 2).subscribe(num => println(s"Doubled: $num"))
     }
   }
   ```

71. **Create a Scheduler:**
   Implement a task scheduler that executes tasks at specified intervals.
   ```scala
   import scala.concurrent.duration._
   import scala.concurrent.ExecutionContext.Implicits.global
   import scala.concurrent.Future

   object Scheduler {
     def schedule(task: () => Unit, interval: FiniteDuration): Unit = {
       Future {
         while (true) {
           task()
           Thread.sleep(interval.toMillis)
         }
       }
     }

     // Example usage:
     // schedule(() => println("Task executed!"), 1.second)
   }
   ```

72. **Implement a Search Engine:**
   Create a basic search engine that indexes and searches text documents.
   ```scala
   import scala.collection.mutable

   class SearchEngine {
     private val index = mutable.Map[String, List[String]]()

     def indexDocument(id: String, text: String): Unit = {
       text.split("\\W+").foreach { word =>
         val lowerWord = word.toLowerCase
         val ids = index.getOrElse(lowerWord, List())
         index(lowerWord) = id :: ids
       }
     }

     def search(query: String): List[String] = {
       index.getOrElse(query.toLowerCase, List())
     }
   }

   // Example usage:
   // val engine = new SearchEngine
   // engine.indexDocument("1", "Hello World")
   // println(engine.search("hello")) // Output: List(1)
   ```

73. **File Encryption:**
   Implement a basic file encryption/decryption algorithm.
   ```scala
   import java.nio.file.{Files, Paths}
   import javax.crypto.Cipher
   import javax.crypto.spec.SecretKeySpec

   object FileEncryptor {
     private val ALGORITHM = "AES"
     private val key = "1234567890123456" // 16 byte key

     def encrypt(inputFile: String, outputFile: String): Unit = {
       val cipher = Cipher.getInstance(ALGORITHM)
       cipher.init(Cipher.ENCRYPT_MODE, new SecretKeySpec(key.getBytes, ALGORITHM))

       val inputBytes = Files.readAllBytes(Paths.get(inputFile))
       val outputBytes = cipher.doFinal(inputBytes)

       Files.write(Paths.get(outputFile), outputBytes)
     }

     def decrypt(inputFile: String, outputFile: String): Unit = {
       val cipher = Cipher.getInstance(ALGORITHM)
       cipher.init(Cipher.DECRYPT_MODE, new SecretKeySpec(key.getBytes, ALGORITHM))

       val inputBytes = Files.readAllBytes(Paths.get(inputFile))
       val outputBytes = cipher.doFinal(inputBytes)

       Files.write(Paths.get(outputFile), outputBytes)
     }
   }
   ```

74. **Implement Graph Algorithms:**
   Write functions to implement common graph algorithms (e.g., BFS, DFS).
   ```scala
   import scala.collection.mutable

   case class Graph(adjList: Map[Int, List[Int]]) {
     def bfs(start: Int): List[Int] = {
       val visited = mutable.Set[Int]()
       val queue = mutable.Queue[Int](start)
       val result = mutable.ListBuffer[Int]()

       while (queue.nonEmpty) {
         val node = queue.dequeue()
         if (!visited(node)) {
           visited.add(node)
           result += node
           queue.enqueue(adjList.getOrElse(node, List()): _*)
         }
       }
       result.toList
     }
   }

   // Example usage:
   // val graph = Graph(Map(1 -> List(2, 3), 2 -> List(4), 3 -> List(4), 4 -> List()))
   // println

(graph.bfs(1)) // Output: List(1, 2, 3, 4)
   ```

75. **Build a Simple E-commerce Application:**
   Create a basic e-commerce application with product listings and a shopping cart.
   ```scala
   case class Product(id: Int, name: String, price: Double)
   case class Cart(items: List[Product]) {
     def add(product: Product): Cart = copy(items = product :: items)
     def totalPrice: Double = items.map(_.price).sum
   }

   object ECommerce {
     var products = List(
       Product(1, "Apple", 0.5),
       Product(2, "Banana", 0.3)
     )

     def listProducts(): Unit = {
       println("Available Products:")
       products.foreach(p => println(s"${p.id}: ${p.name} - ${p.price}"))
     }

     def main(args: Array[String]): Unit = {
       listProducts()
       var cart = Cart(List())
       cart = cart.add(products.head)
       println(s"Total Price: ${cart.totalPrice}")
     }
   }
   ```

---

### **Example Implementations**

#### **Haskell Example: List Reversal**

```haskell
reverseList :: [a] -> [a]
reverseList = foldl (flip (:)) []
```

#### **Scala Example: List Reversal**

```scala
def reverseList[A](list: List[A]): List[A] = list.foldLeft(List.empty[A])((acc, elem) => elem :: acc)
```

#### **Haskell Example: Matrix Multiplication**

```haskell
type Matrix = [[Int]]

multiplyMatrices :: Matrix -> Matrix -> Matrix
multiplyMatrices a b = [[ sum $ zipWith (*) ar bc | bc <- transpose b ] | ar <- a]
```

#### **Scala Example: Matrix Multiplication**

```scala
def multiplyMatrices(a: Array[Array[Int]], b: Array[Array[Int]]): Array[Array[Int]] = {
  val rowsA = a.length
  val colsA = a(0).length
  val colsB = b(0).length
  val c = Array.ofDim[Int](rowsA, colsB)
  
  for (i <- 0 until rowsA; j <- 0 until colsB) {
    c(i)(j) = (0 until colsA).map(k => a(i)(k) * b(k)(j)).sum
  }
  
  c
}
```
