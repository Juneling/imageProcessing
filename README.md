# imageProcessing
#include<iostream>
#include<opencv2/opencv.hpp>
#include<opencv2/highgui.hpp>
using namespace std;
using namespace cv;
typedef Vec<uchar, 3> Vec3b;
int main(int arc, char* argv[])
{
	/***************图片读取，读取灰度值，显示****************/
	Mat img = imread("E:/Pic/girl.jpg",0);// 读入一张图片（游戏原画）
	Mat result;
	Canny(img, result, 0, 200);
	imwrite("E:/Pic/girl_canny.png", result);
	imshow("result", result);
	waitKey(0);
	
	/******************视频读取******************/
	VideoCapture cap("E:/xunlei/Game.Of.Thrones.S03.Season.3/GTS03E01.mp4");
	if (!cap.isOpened()){
		cout << "cannot open the video file" << endl;
		return -1;
	}
	Mat edge;
	namedWindow("edge", 1);
	string s = "Picture";
	for (int i=0;;i++){
		Mat frame;
		cap >> frame;//从cap中读一帧，存到frame中
		if (frame.empty())break;
		//imwrite("E:/xunlei/Game.Of.Thrones.S03.Season.3/string.png", frame);
		cvtColor(frame, edge, CV_BGR2GRAY);
		Canny(edge, edge, 0, 30, 3);
		imshow("edge", edge);
		if (waitKey(50) >= 0)
			break;
	}
	
	/*Mat M(10, 8, CV_8UC3, Scalar(100, 60, 190));
	cout << M;
	cout << endl;
	imshow("Selfdesign", M);
	waitKey(0);*/

	/*cout << img.size << endl;
	cout << img.cols << endl;
	cout << img.rows << endl;
	Mat grayIm(400, 400, CV_8UC3);
	Mat colorIm(600, 800, CV_8UC3);
	for (int i = 0; i < grayIm.rows;i++)
		for (int j = 0; j < grayIm.cols; j++)
		{
			grayIm.at<uchar>(i, j) = img.at<uchar>(i, j);
		}
	imshow("grayIm",grayIm);
	waitKey(0);*/

	return 0;
}
