package KNN;

import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.Map;
import java.util.TreeMap;
import java.util.stream.Collectors;

import Vector.Vector;

public class Knn {
	private List<Vector> trainSet = new ArrayList<>();
	private List<Vector> testSet = new ArrayList<>();

	public static void main(String[] args) throws FileNotFoundException {
		Knn knn = new Knn(Knn.class.getResource("/KNN/train.txt").getFile(),
				Knn.class.getResource("/KNN/test.txt").getFile());
		for (int i = 1; i <= 121; i += 5)
			System.out.println("K=" + i + ", accuracy is: " + knn.accuracy(i) * 100 + "%");

	}

	public Knn(String train, String test) throws FileNotFoundException {
		trainSet = Vector.vectorParser(train);
		testSet = Vector.vectorParser(test);
	}

	public double accuracy(int k) {
		int errorCount = 0;
		for (Vector test : testSet) {
			Map<Vector, Double> m = new TreeMap<>();
			for (Vector train : trainSet) {
				double distance = Math.sqrt(powTwo(train.x - test.x) + powTwo(train.y - test.y)
						+ powTwo(train.z - test.z) + powTwo(train.t - test.t));
				m.put(train, distance);
			}
			String maxOccurancyClass = m.entrySet().stream()
					.sorted(Comparator.comparing(Map.Entry<Vector, Double>::getValue)).limit(k)
					.map(a -> a.getKey().className).collect(Collectors.groupingBy(p -> p, Collectors.counting()))
					.entrySet().stream().max(Comparator.comparing(Map.Entry<String, Long>::getValue))
					.map(Map.Entry::getKey).get();
			errorCount += test.className.equals(maxOccurancyClass) ? 0 : 1;
		}
		return (double) (testSet.size() - errorCount) / testSet.size();
	}

	public static double powTwo(double a) {
		return a * a;
	}

}
