## 1. Getting Started

**Concept:**
Getting started with Haskell involves setting up the environment, learning the basics of Haskell syntax, and writing simple programs.

**Setup:**
- **Install GHC:** The Glasgow Haskell Compiler (GHC) is the most commonly used compiler for Haskell.
- **Install Cabal:** The Cabal build tool helps manage Haskell packages and projects.
- **IDE:** Use an IDE or editor like VSCode with the Haskell extension or IntelliJ IDEA with the Haskell plugin for enhanced development.

**Basic Haskell Syntax:**
- Define functions using `functionName args = expression`
- Use `let` and `in` for local bindings.

**Example:**

```haskell
-- A simple function to add two numbers
add :: Int -> Int -> Int
add x y = x + y

main :: IO ()
main = do
  let sum = add 3 5
  print sum
```

**Real-World Example:**

Creating a simple calculator program:

```haskell
-- Function to perform addition
add :: Int -> Int -> Int
add x y = x + y

-- Function to perform subtraction
subtract :: Int -> Int -> Int
subtract x y = x - y

-- Main function to use the calculator
main :: IO ()
main = do
  let result1 = add 10 5
  let result2 = subtract 10 5
  putStrLn ("Addition result: " ++ show result1)
  putStrLn ("Subtraction result: " ++ show result2)
```

---

## 2. Types and Functions

**Concept:**
Understanding Haskell’s type system and how functions are defined and used.

**Types:**
- **Basic Types:** `Int`, `Float`, `Char`, `Bool`
- **Custom Types:** Define new types using `data` or `newtype`.

**Functions:**
- **Type Signatures:** Define the input and output types of functions.
- **Currying:** Functions in Haskell are curried by default.

**Example:**

```haskell
-- Type signature for a function that calculates the area of a rectangle
area :: Float -> Float -> Float
area width height = width * height

-- Function using currying
add :: Int -> Int -> Int
add x y = x + y
```

**Real-World Example:**

Defining a function for calculating the Body Mass Index (BMI):

```haskell
-- Function to calculate BMI
bmi :: Float -> Float -> String
bmi weight height
  | bmiValue < 18.5 = "Underweight"
  | bmiValue < 25.0 = "Normal weight"
  | bmiValue < 30.0 = "Overweight"
  | otherwise = "Obesity"
  where bmiValue = weight / (height * height)
```

---

## 3. Defining Types, Streamlining Functions

**Concept:**
Creating custom data types and simplifying function definitions for better code organization.

**Custom Types:**
- **Data Types:** Use `data` to define new types.
- **Type Synonyms:** Use `type` to create synonyms for existing types.

**Example:**

```haskell
-- Define a custom data type for a Person
data Person = Person { name :: String, age :: Int }

-- Function to create a greeting message
greet :: Person -> String
greet (Person n a) = "Hello, " ++ n ++ ". You are " ++ show a ++ " years old."
```

**Real-World Example:**

Defining a type for an address and creating a function to format it:

```haskell
-- Define a custom data type for Address
data Address = Address { street :: String, city :: String, zipCode :: String }

-- Function to format Address
formatAddress :: Address -> String
formatAddress (Address s c z) = s ++ ", " ++ c ++ " " ++ z
```

---

## 4. Functional Programming

**Concept:**
Exploring the principles of functional programming in Haskell, such as immutability, higher-order functions, and pure functions.

**Principles:**
- **Immutability:** Data is immutable; once created, it cannot be changed.
- **Higher-Order Functions:** Functions that take other functions as arguments or return functions.

**Example:**

```haskell
-- Higher-order function that applies a function to a list of integers
applyFunction :: (Int -> Int) -> [Int] -> [Int]
applyFunction f xs = map f xs

-- Example usage
incrementedNumbers = applyFunction (+1) [1, 2, 3]
```

**Real-World Example:**

Using higher-order functions to process a list of names:

```haskell
-- Function to capitalize names
capitalize :: String -> String
capitalize (x:xs) = toUpper x : xs

-- Applying capitalize to a list of names
capitalizeNames :: [String] -> [String]
capitalizeNames = map capitalize
```

---

## 5. Writing a Library: Working with JSON Data

**Concept:**
Creating a library to handle JSON data using Haskell libraries like `aeson` for JSON parsing and encoding.

**Example:**

```haskell
{-# LANGUAGE OverloadedStrings #-}

import Data.Aeson (FromJSON, ToJSON, decode, encode, parseJSON, toJSON)
import Data.Text (Text)

-- Define a data type for a person
data Person = Person { name :: String, age :: Int } deriving (Show, Generic)

instance FromJSON Person
instance ToJSON Person

-- Encode and decode functions
encodePerson :: Person -> ByteString
encodePerson = encode

decodePerson :: ByteString -> Maybe Person
decodePerson = decode
```

**Real-World Example:**

Parsing a JSON file to extract user data:

```haskell
import Data.Aeson
import qualified Data.ByteString.Lazy as B

-- Function to read and parse JSON file
parseUserFile :: FilePath -> IO (Maybe Person)
parseUserFile filePath = do
  jsonData <- B.readFile filePath
  return (decode jsonData :: Maybe Person)
```

---

## 6. Using Typeclasses

**Concept:**
Typeclasses allow for polymorphism by defining a set of functions that can operate on various types.

**Example:**

```haskell
-- Define a typeclass for Printable types
class Printable a where
  printValue :: a -> String

-- Implement Printable for Int
instance Printable Int where
  printValue = show

-- Implement Printable for Person
instance Printable Person where
  printValue (Person n a) = "Name: " ++ n ++ ", Age: " ++ show a
```

**Real-World Example:**

Creating a typeclass for a generic `describe` function:

```haskell
class Describable a where
  describe :: a -> String

instance Describable Person where
  describe (Person n a) = "Person named " ++ n ++ " who is " ++ show a ++ " years old."
```

---

## 7. Input and Output

**Concept:**
Handling input and output operations, including reading from and writing to files and standard input/output.

**Example:**

```haskell
import System.IO

-- Reading from a file
readFileContent :: FilePath -> IO String
readFileContent path = do
  content <- readFile path
  return content

-- Writing to a file
writeFileContent :: FilePath -> String -> IO ()
writeFileContent path content = writeFile path content

-- Reading from standard input
getUserInput :: IO String
getUserInput = do
  putStrLn "Enter your name:"
  name <- getLine
  return name
```

**Real-World Example:**

Reading a file and processing its content:

```haskell
import System.IO

-- Function to count the number of lines in a file
countLines :: FilePath -> IO Int
countLines path = do
  contents <- readFile path
  return (length (lines contents))
```

---

## 8. Efficient File Processing, Regular Expressions, and File Name Matching

**Concept:**
Efficient file processing, using regular expressions for pattern matching, and handling file names.

**Example:**

```haskell
import System.Directory
import System.FilePath
import Text.Regex.Posix

-- List all files in a directory matching a pattern
listMatchingFiles :: FilePath -> String -> IO [FilePath]
listMatchingFiles dir pattern = do
  files <- listDirectory dir
  return [ file | file <- files, file =~ pattern ]
```

**Real-World Example:**

Using regular expressions to extract email addresses from a file:

```haskell
import Text.Regex.Posix

-- Extract email addresses from text
extractEmails :: String -> [String]
extractEmails text = getAllTextMatches (text =~ "\\b[\\w.]+@[\\w.]+\\b" :: AllTextMatches [] String)
```

---

## 9. I/O Case Study: A Library for Searching the Filesystem

**Concept:**
Building a library to perform filesystem operations, such as searching for files and directories.

**Example:**

```haskell
import System.Directory
import System.FilePath

-- Function to search for files with a specific extension
searchFilesWithExtension :: FilePath -> String -> IO [FilePath]
searchFilesWithExtension dir ext = do
  files <- listDirectory dir
  let matchedFiles = filter (\f -> takeExtension f == ext) files
  return matchedFiles
```

**Real-World Example:**

Creating a

 library to search for specific files:

```haskell
import System.Directory
import System.FilePath

-- Recursive function to search files
searchFiles :: FilePath -> String -> IO [FilePath]
searchFiles dir pattern = do
  contents <- listDirectory dir
  let files = map (dir </>) contents
  dirs <- filterM doesDirectoryExist files
  files' <- filterM doesFileExist files
  matchedFiles <- filterM (return . (pattern `isInfixOf`)) files'
  subDirs <- mapM (\d -> searchFiles d pattern) dirs
  return (matchedFiles ++ concat subDirs)
```

---

## 10. Code Case Study: Parsing a Binary Data Format

**Concept:**
Parsing binary data formats using Haskell’s libraries and techniques.

**Example:**

```haskell
import Data.Binary.Get
import Data.Word

-- Parsing a binary format
parseBinaryData :: Get (Word8, Word16)
parseBinaryData = do
  byte <- getWord8
  word <- getWord16be
  return (byte, word)
```

**Real-World Example:**

Reading a custom binary file format:

```haskell
import Data.Binary.Get
import qualified Data.ByteString.Lazy as B

-- Read and parse a binary file
readBinaryFile :: FilePath -> IO (Word8, Word16)
readBinaryFile path = do
  content <- B.readFile path
  return $ runGet parseBinaryData content
```

---

## 11. Testing and Quality Assurance

**Concept:**
Writing tests and ensuring code quality using Haskell’s testing frameworks.

**Example:**

```haskell
import Test.HUnit

-- Define a test case
testAdd :: Test
testAdd = TestCase (assertEqual "for (add 1 2)," 3 (add 1 2))

-- Run the tests
main :: IO ()
main = runTestTT testAdd >>= print
```

**Real-World Example:**

Using Hspec for testing:

```haskell
import Test.Hspec

-- Define a spec
spec :: Spec
spec = do
  describe "add" $ do
    it "adds two numbers" $ do
      add 1 2 `shouldBe` 3

-- Run the tests
main :: IO ()
main = hspec spec
```

---

## 12. Barcode Recognition

**Concept:**
Implementing barcode recognition using Haskell.

**Example:**

Using libraries like `zxing` for barcode scanning:

```haskell
import Codec.Picture
import Codec.Picture.Types

-- Dummy function to represent barcode recognition
recognizeBarcode :: FilePath -> IO (Maybe String)
recognizeBarcode filePath = do
  image <- readImage filePath
  return $ Just "123456789"  -- Placeholder implementation
```

**Real-World Example:**

Reading a barcode image:

```haskell
import Codec.Picture

-- Function to read barcode from an image file
readBarcode :: FilePath -> IO (Maybe String)
readBarcode filePath = do
  img <- readImage filePath
  case img of
    Left err -> return Nothing
    Right (ImageY8 image) -> return $ Just "barcode-data"  -- Placeholder
    _ -> return Nothing
```

---

## 13. Data Structures

**Concept:**
Exploring various data structures in Haskell, including lists, trees, and maps.

**Example:**

```haskell
-- Define a binary tree
data Tree a = Empty | Node a (Tree a) (Tree a) deriving Show

-- Function to insert into a binary tree
insert :: Ord a => a -> Tree a -> Tree a
insert x Empty = Node x Empty Empty
insert x (Node y left right)
  | x < y     = Node y (insert x left) right
  | otherwise = Node y left (insert x right)
```

**Real-World Example:**

Using `Data.Map` for a key-value store:

```haskell
import qualified Data.Map as Map

-- Creating and using a map
exampleMap :: Map.Map String Int
exampleMap = Map.fromList [("apple", 1), ("banana", 2)]

-- Lookup in the map
lookupValue :: String -> Maybe Int
lookupValue key = Map.lookup key exampleMap
```

---

## 14. Monads

**Concept:**
Understanding monads and their use in Haskell for chaining operations and handling side effects.

**Example:**

```haskell
-- The Maybe Monad
example :: Maybe Int
example = do
  x <- Just 10
  y <- Just 20
  return (x + y)
```

**Real-World Example:**

Using `IO` monad for side effects:

```haskell
-- Function to read and print an integer from the user
readAndPrintInt :: IO ()
readAndPrintInt = do
  putStrLn "Enter a number:"
  input <- getLine
  let number = read input :: Int
  print number
```

---

## 15. Programming with Monads

**Concept:**
Using monads to manage computations and side effects more effectively.

**Example:**

```haskell
-- Using the State Monad
import Control.Monad.State

type Counter = State Int

increment :: Counter ()
increment = do
  count <- get
  put (count + 1)

runCounter :: Int -> ((), Int)
runCounter initial = runState (increment >> increment) initial
```

**Real-World Example:**

Building a stateful computation:

```haskell
-- Define a stateful computation to track a counter
type Counter = State Int

addToCounter :: Int -> Counter ()
addToCounter n = do
  count <- get
  put (count + n)

runCounterExample :: Int -> Int -> Int
runCounterExample start incrementBy = evalState (addToCounter incrementBy >> get) start
```

---

## 16. The Parsec Parsing Library

**Concept:**
Using the Parsec library for constructing parsers in Haskell.

**Example:**

```haskell
import Text.Parsec
import Text.Parsec.String (Parser)

-- Define a parser for integers
integerParser :: Parser Int
integerParser = read <$> many1 digit

-- Define a parser for a simple expression
expressionParser :: Parser Int
expressionParser = do
  x <- integerParser
  spaces
  char '+'
  spaces
  y <- integerParser
  return (x + y)
```

**Real-World Example:**

Parsing a configuration file:

```haskell
import Text.Parsec
import Text.Parsec.String (Parser)

-- Parser for a key-value pair
keyValuePair :: Parser (String, String)
keyValuePair = do
  key <- many1 (alphaNum <|> char '_')
  spaces
  char '='
  spaces
  value <- many1 (alphaNum <|> char '_')
  return (key, value)

-- Parse a list of key-value pairs
parseConfig :: String -> Either ParseError [(String, String)]
parseConfig = parse (keyValuePair `sepEndBy` newline) ""
```

---

## 17. The Foreign Function Interface

**Concept:**
Using Haskell’s Foreign Function Interface (FFI) to call functions from other languages like C.

**Example:**

```haskell
{-# LANGUAGE ForeignFunctionInterface #-}

import Foreign.C.Types

-- Foreign function declaration
foreign import ccall "math.h sin"
  c_sin :: CDouble -> IO CDouble

-- Haskell function to use the foreign function
calculateSin :: Double -> IO Double
calculateSin x = do
  result <- c_sin (realToFrac x)
  return (realToFrac result)
```

**Real-World Example:**

Calling a C library function to perform a calculation:

```haskell
{-# LANGUAGE ForeignFunctionInterface #-}

import Foreign.C.Types

foreign import ccall "math.h pow"
  c_pow :: CDouble -> CDouble -> IO CDouble

-- Use the foreign function
power :: Double -> Double -> IO Double
power base exponent = do
  result <- c_pow (realToFrac base) (realToFrac exponent)
  return (realToFrac result)
```

---

## 18. Monad Transformers

**Concept:**
Using monad transformers to combine multiple monads, allowing for complex computations with different effects.

**Example:**

```haskell
import Control.Monad.Trans.State
import Control.Monad.Trans.Class (lift)
import Control.Monad.IO.Class (liftIO)

type MyState = StateT Int IO

-- Function to increment state and print a message
incrementAndPrint :: MyState ()
incrementAndPrint = do
  liftIO $ putStrLn "Incrementing state"
  count <- get
  put (count + 1)

-- Running the stateful computation
runMyState :: IO ()
runMyState = evalStateT incrementAndPrint 0
```

**Real-World Example:**

Combining `StateT` and `IO` monads to handle state and I/O:

```haskell
import Control.Monad.Trans.State
import Control.Monad.IO.Class (liftIO)

type AppState = StateT Int IO

-- Function that uses state and performs I/O
appFunction :: AppState ()
appFunction = do
  liftIO $ putStrLn "Performing action"
  count <- get
  liftIO $ putStrLn ("Current count: " ++ show count)
  put (count + 1)

-- Running the application
runApp :: IO ()
runApp = evalStateT appFunction 0
```

---

## 19. Error Handling

**Concept:**
Handling errors gracefully in Haskell using

 techniques like `Either`, `Maybe`, and `MonadError`.

**Example:**

```haskell
-- Function that uses Either for error handling
divide :: Double -> Double -> Either String Double
divide _ 0 = Left "Division by zero"
divide x y = Right (x / y)
```

**Real-World Example:**

Handling file errors:

```haskell
import System.IO.Error (tryIOError, IOError)

-- Function to read a file and handle errors
safeReadFile :: FilePath -> IO (Either IOError String)
safeReadFile path = tryIOError (readFile path)
```

---

## 20. Systems Programming

**Concept:**
Performing low-level systems programming tasks such as interacting with operating system facilities and hardware.

**Example:**

```haskell
import System.Posix.Types
import System.Posix.Files

-- Check if a file is executable
isExecutable :: FilePath -> IO Bool
isExecutable path = do
  status <- getFileStatus path
  return $ fileMode status `mod` 2 == 1
```

**Real-World Example:**

Interacting with environment variables:

```haskell
import System.Environment (getEnv)

-- Function to get an environment variable
getEnvVar :: String -> IO (Maybe String)
getEnvVar var = do
  result <- try (getEnv var) :: IO (Either IOError String)
  return (either (const Nothing) Just result)
```

---

## 21. Working with Databases

**Concept:**
Interacting with databases using Haskell libraries such as `persistent` or `sqlite`.

**Example:**

```haskell
{-# LANGUAGE OverloadedStrings #-}

import Database.SQLite.Simple

-- Connect to a database
connectDB :: IO Connection
connectDB = open "test.db"

-- Create a table
createTable :: Connection -> IO ()
createTable conn = execute_ conn "CREATE TABLE IF NOT EXISTS person (id INTEGER PRIMARY KEY, name TEXT)"

-- Insert a record
insertPerson :: Connection -> String -> IO ()
insertPerson conn name = execute conn "INSERT INTO person (name) VALUES (?)" (Only name)
```

**Real-World Example:**

Querying data from a database:

```haskell
{-# LANGUAGE OverloadedStrings #-}

import Database.SQLite.Simple

-- Query all persons from the database
queryAllPersons :: Connection -> IO [String]
queryAllPersons conn = do
  rows <- query_ conn "SELECT name FROM person" :: IO [Only String]
  return (map fromOnly rows)
```

---

## 22. Web Client Programming

**Concept:**
Creating web clients to interact with web services using Haskell libraries such as `http-client` or `wreq`.

**Example:**

```haskell
import Network.HTTP.Client
import Network.HTTP.Client.TLS (tlsManagerSettings)

-- Fetch a web page
fetchPage :: String -> IO String
fetchPage url = do
  manager <- newManager tlsManagerSettings
  request <- parseRequest url
  response <- httpLbs request manager
  return (responseBody response)
```

**Real-World Example:**

Interacting with a REST API:

```haskell
import Network.Wreq
import Control.Lens

-- Perform a GET request
getRequest :: IO ()
getRequest = do
  response <- get "https://api.github.com/repos/haskell/ghc"
  let repoName = response ^. responseBody . key "name" . _String
  print repoName
```

---

## 23. GUI Programming

**Concept:**
Building graphical user interfaces in Haskell using libraries like `gtk` or `threepenny-gui`.

**Example:**

```haskell
import Graphics.UI.Gtk

-- Create a simple GTK window
main :: IO ()
main = do
  initGUI
  window <- windowNew
  set window [windowTitle := "Hello World", windowDefaultWidth := 200, windowDefaultHeight := 100]
  on window destroy mainQuit
  widgetShowAll window
  mainGUI
```

**Real-World Example:**

Building a simple calculator GUI:

```haskell
import Graphics.UI.Gtk

-- Simple calculator example
main :: IO ()
main = do
  initGUI
  window <- windowNew
  button <- buttonNewWithLabel "Click me"
  containerAdd window button
  on button buttonActivated $ putStrLn "Button clicked"
  widgetShowAll window
  mainGUI
```

---

## 24. Basic Concurrent and Parallel Programming

**Concept:**
Performing concurrent and parallel programming in Haskell using `Control.Concurrent` and related libraries.

**Example:**

```haskell
import Control.Concurrent

-- Create two threads that print messages
main :: IO ()
main = do
  forkIO $ putStrLn "Hello from thread 1"
  forkIO $ putStrLn "Hello from thread 2"
  threadDelay 1000000  -- Wait for 1 second
```

**Real-World Example:**

Parallel computation using `async` library:

```haskell
import Control.Concurrent.Async

-- Perform two tasks in parallel
main :: IO ()
main = do
  async1 <- async (putStrLn "Task 1")
  async2 <- async (putStrLn "Task 2")
  wait async1
  wait async2
```

---

## 25. Profiling and Tuning for Performance

**Concept:**
Profiling Haskell programs to identify performance bottlenecks and optimizing code.

**Example:**

```haskell
-- Example of a performance-critical function
longComputation :: Int -> Int
longComputation n = sum [1..n]

-- Use GHC's profiling tools to analyze performance
```

**Real-World Example:**

Using GHC's profiling tools:

1. Compile with profiling enabled: `ghc -prof -rtsopts -o myprogram myprogram.hs`
2. Run the program and generate profiling data: `./myprogram +RTS -p`
3. Analyze the profiling report: `ghc --profile myprogram.prof`

---

## 26. Advanced Library Design: Building a Bloom Filter

**Concept:**
Creating advanced data structures such as Bloom filters for probabilistic data structures.

**Example:**

```haskell
import Data.Bits
import Data.Word
import Data.Hashable

-- Define a Bloom filter
newtype BloomFilter = BloomFilter [Word8]

-- Create a Bloom filter and add elements
addElement :: Hashable a => a -> BloomFilter -> BloomFilter
addElement x (BloomFilter bits) = BloomFilter updatedBits
  where
    hash = hashWithSalt 0 x
    bitIndex = hash `mod` (length bits * 8)
    updatedBits = setBit bits bitIndex
```

**Real-World Example:**

Implementing a Bloom filter for membership testing:

```haskell
import Data.Bits
import Data.Word
import Data.Hashable

-- Bloom filter with basic operations
newtype BloomFilter = BloomFilter [Word8]

addElement :: Hashable a => a -> BloomFilter -> BloomFilter
addElement x (BloomFilter bits) = BloomFilter updatedBits
  where
    hash = hashWithSalt 0 x
    bitIndex = hash `mod` (length bits * 8)
    updatedBits = setBit bits bitIndex

contains :: Hashable a => a -> BloomFilter -> Bool
contains x (BloomFilter bits) = testBit bits bitIndex
  where
    hash = hashWithSalt 0 x
    bitIndex = hash `mod` (length bits * 8)
```

---

## 27. Network Programming

**Concept:**
Network programming in Haskell to create networked applications using libraries such as `network`.

**Example:**

```haskell
import Network.Socket
import Network.Socket.ByteString (recv, sendAll)

-- Simple TCP server
server :: IO ()
server = withSocketsDo $ do
  sock <- socket AF_INET Stream defaultProtocol
  bind sock (SockAddrInet 8080 iNADDR_ANY)
  listen sock 1
  (conn, _) <- accept sock
  msg <- recv conn 1024
  sendAll conn msg
  close conn
```

**Real-World Example:**

Creating a basic HTTP server:

```haskell
import Network.Wai
import Network.Wai.Handler.Warp

-- Simple application that responds with "Hello, World!"
app :: Application
app _respond = respond $ responseLBS status200 [("Content-Type", "text/plain")] "Hello, World!"

-- Run the server
main :: IO ()
main = run 8080 app
```

---

## 28. Software Transactional Memory

**Concept:**
Using Software Transactional Memory (STM) in Haskell for managing concurrent state.

**Example:**

```haskell
import Control.Concurrent.STM
import Control.Concurrent.STM.TMVar

-- Using STM to manage state
main :: IO ()
main = do
  counter <- newTMVarIO 0
  atomically $ do
    value <- takeTMVar counter
    putTMVar counter (value + 1)
```

**Real-World Example:**

Implementing a simple counter with STM:

```haskell
import Control.Concurrent.STM
import Control.Concurrent.STM.TVar

-- Counter with STM
type Counter = TVar Int

incrementCounter :: Counter -> STM ()
incrementCounter counter = do
  value <- readTVar counter
  writeTVar counter (value + 1)

main :: IO ()
main = do
  counter <- newTVarIO 0
  atomically $ incrementCounter counter
  finalValue <- atomically $ readTVar counter
  print finalValue
```

---

## B. Installing G

HC and Setting Up Your Haskell Environment

**Concept:**
Setting up the Haskell development environment on various platforms.

**Example:**

- **Linux/Mac:** Install GHC using the Haskell Platform or GHCup.
- **Windows:** Use the Haskell Platform or GHCup for installation.

**Setup Steps:**

1. **Linux/Mac:**
   - Install GHC and Cabal: `sudo apt-get install ghc cabal-install`
   - Or use GHCup: `curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh`

2. **Windows:**
   - Install the Haskell Platform: Download from [Haskell Platform](https://www.haskell.org/platform/)
   - Or use GHCup: [GHCup for Windows](https://www.haskell.org/ghcup/)

**Real-World Example:**

Creating a new Haskell project with Cabal:

```bash
cabal init
cabal build
cabal run
```

---

## C. Additional Resources

**Concept:**
Resources for further learning and exploring Haskell.

**Books:**

1. "Learn You a Haskell for Great Good!" by Miran Lipovača
2. "Real World Haskell" by Bryan O'Sullivan, Don Stewart, and John Goerzen

**Online Resources:**

1. [Haskell Wiki](https://wiki.haskell.org/)
2. [Haskell Documentation](https://www.haskell.org/documentation/)
