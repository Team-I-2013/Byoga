追加項目
	Mat BGLImage =cv::Mat::zeros(480, 640, CV_8UC3);//描画用 背景を0に指定
	Mat BBLImage =cv::Mat::zeros(480,640,CV_8UC3);

	Mat BGRImage =cv::Mat::zeros(480, 640, CV_8UC3);//描画用 背景を0に指定
	Mat BBRImage =cv::Mat::zeros(480,640,CV_8UC3);

	 cv::bitwise_not(BBLImage, BBLImage);　要素反転　背景を白色に
	cv::bitwise_not(BBRImage, BBRImage);
	
	BBL　→　描画グリーンレフト
	BBR　→　描画ブラックライト
	
	カメラ画像とは別に描画用のものを作りました。
	最後にカメラと描画を合成します。
	
	
	 cv::line(BGLImage,cv::Point(Lx[i],Ly[i]),cv::Point(Lx[i-1],Ly[i-1]),cv::Scalar(0,255,0),8,CV_AA)
	 cv::line(BGRImage,cv::Point(Rx[i],Ry[i]),cv::Point(Rx[i-1],Ry[i-1]),cv::Scalar(0,255,0),8,CV_AA);
	 cv::line(BBLImage,cv::Point(Lx[i],Ly[i]),cv::Point(Lx[i-1],Ly[i-1]),cv::Scalar(0,0,0),8,CV_AA);
	 cv::line(BBRImage,cv::Point(Rx[i],Ry[i]),cv::Point(Rx[i-1],Ry[i-1]),cv::Scalar(0,255,0),8,CV_AA);
	背景が黒の画面に色つき（ここでは仮で緑色にしました。）を描画。　左右両方の画面に描画
	背景が白の画面に黒色を描画
	
	bitwise_and(LdstImage,BBLImage,LdstImage);
	bitwise_and(RdstImage,BBRImage,RdstImage);

	bitwise_or(LdstImage,BGLImage,LdstImage);
	bitwise_or(RdstImage,BGRImage,RdstImage);
	
	論理積　⇒　カメラ画像のまま描画部分のみ黒色に
	論理輪　⇒　論理積で変換した画面の黒色を指定色（今回は緑）　こうすることで何色に指定してもできる
