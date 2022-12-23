using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using OpenCvSharp;

namespace camera
{
    class camera
    {
        static void Main(string[] args)
        {
            VideoCapture video = new VideoCapture(0);
            Mat frame = new Mat();

            while (Cv2.WaitKey(33) != 'q')
            {
                video.Read(frame);
                Mat black_kjs = new Mat();
                Mat dst = frame.Clone();
                Mat blur = new Mat();
                Mat canny = new Mat();
                Mat sobel = new Mat();
                Mat Harris = new Mat();

                Point[][] contours;
                HierarchyIndex[] hierarchy;

                Cv2.InRange(frame, new Scalar(0, 0, 0), new Scalar(80, 80, 80), black_kjs);
                Cv2.FindContours(black_kjs, out contours, out hierarchy, RetrievalModes.External, ContourApproximationModes.ApproxTC89KCOS);

                Cv2.GaussianBlur(frame, blur, new Size(3, 3), 1, 0, BorderTypes.Default);

                Cv2.Sobel(blur, sobel, MatType.CV_32F, 1, 0, ksize: 3, scale: 1, delta: 0, BorderTypes.Default);
                sobel.ConvertTo(sobel, MatType.CV_8UC1);

                Cv2.Canny(blur, canny, 100, 200, 3, true);
                //Cv2.ImShow("hough", canny);

                Cv2.HoughLines(canny, 1, 2, 30);

                //Cv2.CornerHarris(sobel,Harris,2,3,0.4);
                //Cv2.ImShow("Corner", Harris);

                foreach (Point[] p in contours)
                {
                    double length = Cv2.ArcLength(p, true);
                    double area = Cv2.ContourArea(p, true);

                    if (length < 2000) continue;

                    Rect boundingRect = Cv2.BoundingRect(p);
                    Console.WriteLine(boundingRect.Height); //부재 높이
                    Console.WriteLine(boundingRect.Width); //부재 너비

                    //RotatedRect rotatedRect = Cv2.MinAreaRect(p);

                    //for (int j = 0; j < 5; j++)
                    //{
                    //    Cv2.Line(dst, new Point(rotatedRect.Points()[j].X, rotatedRect.Points()[j].Y),
                    //    new Point(rotatedRect.Points()[(j + 1) % 4].X, rotatedRect.Points()[(j + 1) % 4].Y),
                    //    Scalar.Red, 2, LineTypes.AntiAlias);
                    //}

                    //bool convex = Cv2.IsContourConvex(p);
                    //Point[] hull = Cv2.ConvexHull(p, true);
                    //Moments moments = Cv2.Moments(p, false);

                    //Cv2.FillConvexPoly(dst, hull, Scalar.White); //내부
                    //Cv2.Polylines(dst, new Point[][] { hull }, true, Scalar.White, 2);

                    Cv2.Rectangle(dst, boundingRect, Scalar.Red, 2); //직사각형

                }

                //Cv2.DrawContours(dst, new Point[][] { hull }, -1, Scalar.Red, 2); //다각형 왜곽선
                //Cv2.Circle(dst, (int)(moments.M10 / moments.M00), (int)(moments.M01 / moments.M00), 7, Scalar.Red, -1); //질량 중심

            }
            Cv2.ImShow("frame", frame);
            frame.Dispose();
            video.Release();
            Cv2.DestroyAllWindows();
        }
    }
}
