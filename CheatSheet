//start of PGDP 3

//Reading File and Writing File with Buffered
public static void processFile() {
    try (BufferedReader br = new BufferedReader(new FileReader("somefile.txt"));
    BufferedWriter bw = new BufferedWriter(new FileWriter("someotherfile.txt"))) {
    String line = br.readLine();
    while(line != null) {
    if(!line.startsWith("X")) {
    bw.write(line + "\n");
    }
    line = br.readLine();
    }
    } catch (IOException e) {
    System.out.println("Something went wrong");
    }
}
    
    

//Reading File and Writing File with Streams 
public static void processFile() throws IOException {
    List<String> readLines = Files.readAllLines(Path.of("somefile.txt"));
    List<String> linesToWrite = new ArrayList<>();
    for(String line : readLines) {
    if(!line.startsWith("X")) {
    linesToWrite.add(line);
    }
    }
    Files.write(Path.of("someotherfile.txt"), linesToWrite);
}

//Important String Methods

charAt(int index);
length();
substring(int beginIndex, int endIndex);
concat(String str);
trim();
toLowerCase();
toUpperCase();
startsWith(String prefix);
endsWith(String suffix);
contains(CharSequence sequence);
split(String regex);

//Exceptions

    //Predefined Exceptions
    InterruptedException
    IOException
    Exception
    FileNotFoundException


    //Self Defined Exceptions
    // Self defined Exceptions extends the exception class, and other exceptions extends base exceptions
    public class NotEnoughException extends Exception{
        private final int should;
        private final int is;
        public NotEnoughException (int should, int is) {
            if(is >= should) {
                throw new IllegalArgumentException();
            }
            this.should = should;
            this.is = is;
        }
        @Override
        public String toString() {
            return "Should: " + should + ", but is" + is + ".";
        }
    
    }

    public class NotEnoughLetterException extends NotEnoughException{
        public NotEnoughLetterException (int should, int is) {
            super(should, is);
        }
    
        @Override
        public String toString() {
            return "NotLongEnoughException: insufficient length!\n" + super.toString();
        }
    }

    //Methods throw exceptions, which will be handled with the try catch statement. Exceptions can also be propogated by adding 
    //the throw "exception name" keyword

    //finally block runs nevertheless if an exception is caught or not

//Streams

Streams(colletion);
Stream.of(elements);
Arrays.stream(arrayName);
flatMap(); // changing multiple streams into one stream
peek();
filter();
max(Comparator);
min(Comparator);


//Changing streams to map
public static Map<String, Double> delayComparedToTotalTravelTimeByTransport(Stream<TrainConnection> connections) {
    Map<String, List<TrainConnection>> trainConnectionbyType = connections.collect(Collectors.groupingBy(TrainConnection::type));
    return trainConnectionbyType.entrySet().stream().collect(Collectors.
            toMap(Map.Entry::getKey, connectionList -> {
                double totalScheduled = connectionList.getValue().stream().mapToInt(TrainConnection::totalTimeTraveledScheduled).sum();
                double totalTraveled = connectionList.getValue().stream().mapToInt(TrainConnection::totalTimeTraveledActual).sum();
                return (totalTraveled-totalScheduled)/totalTraveled * 100;
            } ));
}

//Comparator Implementation
public static TrainConnection worstDelayedTrain(Stream<TrainConnection> connections) {
    return connections.max(Comparator.comparingInt(tc -> tc.stops().stream().mapToInt(TrainStop::getDelay).max().orElse(0))).orElse(null);
}




//Threads


//Parallel  Multiplication
public void run() {
    if(super.getA().getDimension() <= super.getMinDim()) {
        super.getResults()[super.getThreadID()] = mulSequential(super.getA(), super.getB());
    } else {
        SquareMatrix[] quadrants = new SquareMatrix[8];
        MulComputeThread[] threads = {
                new MulComputeThread(0, super.getA().getQuadrant(1,1), super.getB().getQuadrant(1,1), super.getMinDim(), quadrants),
                new MulComputeThread(1, super.getA().getQuadrant(1,2), super.getB().getQuadrant(2,1), super.getMinDim(), quadrants),
                new MulComputeThread(2, super.getA().getQuadrant(1,1), super.getB().getQuadrant(1,2), super.getMinDim(), quadrants),
                new MulComputeThread(3, super.getA().getQuadrant(1,2), super.getB().getQuadrant(2,2), super.getMinDim(), quadrants),
                new MulComputeThread(4, super.getA().getQuadrant(2,1), super.getB().getQuadrant(1,1), super.getMinDim(), quadrants),
                new MulComputeThread(5, super.getA().getQuadrant(2,2), super.getB().getQuadrant(2,1), super.getMinDim(), quadrants),
                new MulComputeThread(6, super.getA().getQuadrant(2,1), super.getB().getQuadrant(1,2), super.getMinDim(), quadrants),
                new MulComputeThread(7, super.getA().getQuadrant(2,2), super.getB().getQuadrant(2,2), super.getMinDim(), quadrants)

        };

        for(MulComputeThread thread : threads) {
            thread.start();
        }

        for(MulComputeThread thread : threads) {
            try {
                thread.join();
            } catch (InterruptedException e) {
                e.printStackTrace();

            }
        }

        SquareMatrix[] C = new SquareMatrix[4];
        for (int i = 0; i < C.length; i++) {
            C[i] = SquareMatrixAdd.addParallel(quadrants[2*i], quadrants[2*i + 1], super.getMinDim());
        }


        super.getResults()[super.getThreadID()] = new SquareMatrix(C[0],C[1],C[2],C[3]);
} }







    
    









//Multiplying Matrix Sequel
public static SquareMatrix mulSequential(SquareMatrix A, SquareMatrix B) {
    // TODO
    if (A == null) {
        throw new IllegalArgumentException("A can not be null");
    }
    if (B == null) {
        throw new IllegalArgumentException("B can not be null");
    }
    if (A.getDimension() != B.getDimension()) {
        throw new IllegalArgumentException("A and B have different dimensions");
    }
    SquareMatrix C = new SquareMatrix(A.getDimension());

    for (int i = 1; i <= A.getDimension(); i++) {
        for (int j = 1; j <= A.getDimension(); j++) {
            C.set(i, j, BigInteger.ZERO);
            for (int k = 1; k <= A.getDimension(); k++) {
                C.set(i, j, C.get(i, j).add(A.get(i,k).multiply(B.get(k,j))));
            }
        }
    }
    
    return C;
}


//Adding Matrix Sequel
public static SquareMatrix addSequential(SquareMatrix A, SquareMatrix B) {
    if (A == null) {
        throw new IllegalArgumentException("A can not be null");
    }
    if (B == null) {
        throw new IllegalArgumentException("B can not be null");
    }
    if (A.getDimension() != B.getDimension()) {
        throw new IllegalArgumentException("A and B have different dimensions");
    }
    SquareMatrix C = new SquareMatrix(A.getDimension());
    for (int i = 1; i <= A.getDimension(); i++) {
        for (int j = 1; j <= A.getDimension(); j++) {
            C.set(i, j, A.get(i, j).add(B.get(i, j)));
        }
    }
    return C;
}

//Synchronization

//Buffer Creation
public Buffer(int maxSize) {
    if (maxSize < 0)
        throw new IllegalArgumentException(
                "Buffer must have positive size!");
    data = new Exam[maxSize];
    // TODO: Vervollständige diesen Konstruktor
    free = new Semaphore(maxSize);
    occupied = new Semaphore(0);
}

public Exam consume() throws InterruptedException {
    // TODO: Implementiere diese Methode
    Exam e;
    occupied.acquire();
    synchronized (this) {
        e = data[first];
        first = (first+1) % data.length;
    }

    free.release();
    return e;
}

public void produce(Exam e) throws InterruptedException {
    // TODO: Implementiere diese Methode
    free.acquire();
    synchronized (this) {
        data[last] = e;
        last = (last+ 1) % data.length;
    }
    occupied.release();
}

//Synchronized List
public class RW {
    private int readOrWrite = 0;
    public synchronized void startRead() throws InterruptedException{
        while(readOrWrite< 0) {
            wait();
        }
        readOrWrite++;
    }

    public synchronized void endRead() {
        readOrWrite--;
        if(readOrWrite == 0) {
            notify();
        }
    }

    public synchronized void startWrite() throws InterruptedException {
        while(readOrWrite != 0) {
            wait();
        }
        readOrWrite = -1;
    }

    public synchronized void endWrite() {
        readOrWrite = 0;
        notifyAll();
    }
}

public class SynchronizedList<T> {
    private List<T> innerList = new LinkedList<>();
    private RW lock = new RW();

    public void add(int index, T e) throws InterruptedException {
        lock.startWrite();
        innerList.add(index, e);
        lock.endWrite();
    }

    public T remove(int index) throws InterruptedException {
        lock.startWrite();
        T element = innerList.remove(index);
        lock.endWrite();
        return element;
    }

    public T get(int index) throws InterruptedException {
        lock.startRead();
        T element = innerList.get(index);
        lock.endRead();
        return element;
    }

    public boolean contains(T e) throws InterruptedException {
        lock.startRead();
        boolean contains = innerList.contains(e);
        lock.endRead();
        return contains;
    }
}